---
layout: post
title: "C#调用refprop"
tags: 
  - C#
  - refprop
---

C#语言下欲计算热物性，自然想到NIST的refprop库。

refprop是用Fortran写的，搜索了下没有找到好的C#调用实例。

自己试着包装了下，全部代码如下：

{% highlight csharp %}
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Runtime.InteropServices;

namespace RefpropWrapper
{
    public class Refrigerant
    {
        private const int MAXNC = 20; // max number of components

        [DllImport("refprop.dll", EntryPoint = "TRNPRPdll", SetLastError = true)]
        private static extern void TRNPRPdll(
            ref double temperature, ref double density, [In, Out] double[] composition,
            [In, Out] ref double viscosity, [In, Out] ref double thermalConductivity,
            [In, Out] ref int ierr, [In, Out] char[] herr, int l1);
        public struct TrnPrpResult
        {
            /// <summary>
            /// [uPa.s]
            /// </summary>
            public double Viscosity;
            /// <summary>
            /// [W/m.K]
            /// </summary>
            public double ThermalConductivity;
        }
        /// <summary>
        /// compute the transport properties of thermal conductivity and
        /// viscosity as functions of temperature and density
        /// </summary>
        /// <param name="fluid"></param>
        /// <param name="composition"></param>
        /// <param name="temperature">[K]</param>
        /// <param name="density">[mol/L]</param>
        /// <returns></returns>
        public static TrnPrpResult GetTrnPrp(string[] fluid, double[] composition, double temperature, double density)
        {
            Setup(fluid);
            double viscosity = 0;
            double thermalConductivity = 0;
            int ierr = 0;
            char[] herr = new char[256];
            TRNPRPdll(ref temperature, ref density, composition, ref viscosity, ref thermalConductivity, ref ierr, herr, herr.Length);
            return new TrnPrpResult { Viscosity = viscosity, ThermalConductivity = thermalConductivity };
        }


        [DllImport("refprop.dll", EntryPoint = "SATPdll", SetLastError = true)]
        private static extern void SATPdll(
            ref double pressure, [In, Out] double[] composition, ref Int32 phase,
            [In, Out] ref double temperature, [In, Out] ref double densityL, [In, Out] ref double densityV, [Out] double[] compositionL, [Out] double[] compositionV,
            [In, Out] ref int ierr, [In, Out] char[] herr, int l1);
        public struct SatPResult
        {
            /// <summary>
            /// [K]
            /// </summary>
            public double Temperature;
            /// <summary>
            /// 
            /// </summary>
            public double DensityL;
            /// <summary>
            /// 
            /// </summary>
            public double DensityV;
        }
        public static SatPResult GetSatP(string[] fluid, double[] composition, double pressure)
        {
            Setup(fluid);
            int phase = 2; // Phase: Vapor
            double temperature = 0.0;
            double densityL = 0.0;
            double densityV = 0.0;
            double[] compositionL = new double[MAXNC];
            double[] compositionV = new double[MAXNC];
            int ierr = 0;
            char[] herr = new char[256];
            SATPdll(ref pressure, composition, ref phase, ref temperature, ref densityL, ref densityV, compositionL, compositionV, ref ierr, herr, herr.Length);
            return new SatPResult { Temperature = temperature, DensityL = densityL, DensityV = densityV };
        }


        // Below: refprop setup stuff =======================================================
        [DllImport("refprop.dll", EntryPoint = "SETUPdll", SetLastError = true)]
        private static extern void SETUPdll(ref int nc, string hfiles, string hfmix, string hrf, ref int ierr, [In, Out] char[] herr, int l1, int l2, int l3, int l4);

        [DllImport("refprop.dll", EntryPoint = "SETMIXdll", SetLastError = true)]
        private extern static void SETMIXdll(string hmxnme, string hfmix, string hrf, ref int nc, [In, Out] char[] hfiles, [In, Out] double[] x, ref int ierr, [In, Out] char[] herr, int l1, int l2, int l3, int l4, int l5);

        [DllImport("refprop.dll", EntryPoint = "SETPATHdll", SetLastError = true)]
        private static extern void SETPATHdll(string path, int l);

        private static string _oldComponents = "";
        private static void Setup(string[] components)
        {
            if (components.Length > MAXNC) throw new Exception("Too many components.");
            // only setup once for same components
            if (!string.IsNullOrEmpty(_oldComponents)
                && string.Join("#", components) == _oldComponents) return;
            _oldComponents = string.Join("#", components);

            string fluidsdir = "fluids/";
            SETPATHdll(fluidsdir, fluidsdir.Length);
            string mixturesdir = "mixtures/";
            //string hrf = "OT0";
            string hrf = "DEF";
            string hfmix = "HMX.BNC";

            if (components.Length == 1 && components[0].ToUpper().Contains(".MIX"))
            { // pre-defined mixed (.mix)
                string hmxnme = mixturesdir + components[0];

                int nc = 0;
                int ierr = 0;
                char[] herr = new char[256];
                char[] fluids = new char[5000]; // 5000 is big enough, too small will raise exception from refprop.dll
                double[] x = new double[MAXNC];

                SETMIXdll(hmxnme, hfmix, hrf, ref nc, fluids, x, ref ierr, herr,
                    hmxnme.Length, hfmix.Length, hrf.Length, fluids.Length, herr.Length);
                if (ierr < 0)
                { // < 0 error; > 0 warning
                    throw new Exception(new string(herr));
                }
            }
            else
            {// pure & user-defined mixed (.fld); pseudo-pure fluid (.ppf)
                int nc = components.Length;
                string fluids = "";
                if (nc == 1)
                { // pure (.fld) & pseudo-pure fluid (.ppf)
                    fluids = components[0];
                }
                else
                { // user-defined mixed (a.fld|b.fld|c.fld|)
                    fluids = string.Join("|", components) + "|"; // postfix "|" is needed
                }

                int ierr = 0;
                char[] herr = new char[256];

                SETUPdll(ref nc, fluids, hfmix, hrf, ref ierr, herr,
                    fluids.Length, hfmix.Length, hrf.Length, herr.Length);
                if (ierr < 0)
                { // < 0 error; > 0 warning
                    throw new Exception(new string(herr));
                }
            }
        }

    }
}
{% endhighlight %}

以上仅包装了两个方法，其它的包装方法类似，苦力。。。

使用方式大概如下代码：

{% highlight csharp %}
string[] component = new string[] { "R32", "R125" };
double[] proportion = new double[] { 0.69762, 0.30238 };
var r = Base.Refrigerant.GetTrnPrp(component, proportion, 300, 2);
MessageBox.Show(r.ThermalConductivity.ToString());
{% endhighlight %}

友情提醒：

* 别忘了把refprop.dll以及fluids和mixtures拷贝到程序目录下
* refprop版本是9.0
* Visual Studio 2010测试通过

参考资料：

[http://www.boulder.nist.gov/div838/theory/refprop/Frequently_asked_questions.htm](http://www.boulder.nist.gov/div838/theory/refprop/Frequently_asked_questions.htm)