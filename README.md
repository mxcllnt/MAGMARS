# MAGMARS
Ref: 	
[A] Collinet et al. 2021 JGR:P; MAGMARS: a Melting Model for the Martian Mantle and FeO-rich Peridotite

[B] Collinet et al. 2023 GRL; The temperature and composition of the mantle sources of Martian basalts
	
(1), (2) and (3) are contained in the compressed folder MAGMARS_model_v1.zip

(6), (7) and (8) are the full supporting information for Collinet et al. (2023)

-----------------------------------------------------------------------------------
(1) MAGMARS melting model package

MAGMARS simulates the melting of FeO-peridotite (e.g. the martian mantle)

The package contains: 
- MAGMARS_v1.m 
- MM_reg.m
- MM_modecalc.m
- WeighObs.m
- lherzolite_reg.txt
- harzburgite_reg.txt

The function MM_reg produces the required linear regressions from the experimental database (lherzolite_reg.txt and harzburgite_reg.txt) and allow to put different weight on experiments (1st column) by calling WeighObs.m

MAGMARS_v1.m requires the following inputs: 

   inputs: |O| name (string) 
	   |1| Start_P (in GPa)         |2| End_P (in GPa)
           |3| Bulk_Comp, Mantle composition (oxide vector, wt%, 1x11)  [SiO2 TiO2 Al2O3 Cr2O3 FeO MnO MgO CaO Na2O K2O P2O5]
           |4| CMF = critical melt fraction (0.004-0.02)
           |5,6,7| Tp_min, Tp_inc, Tp_max (ºC) decompression melting along adiabat(s)
               e.g. 1300,0,1300 for a single adiabat at 1300, etc.
           |8| Iso_mode 1 (True) or 0 (False); default (False) = polybaric melting
           |9| KD [4,0.35] is recommended, or [2,0.35], usually not necessary to change
           |10| T_continuous. [0 X] no, except above temperature X -> harz. temperature
               [1 X] yes always, optimized for harz. melting [2 X] optimized for lherz, not recommended for high melt fractions
               default: [0 1300]
           |11| plotit = 1, then plot figure, = 0 don't plot for better perf.

[Final_table,Final_residue,detail_comp,detail_comp2] = MAGMARS_v1(name,Start_P,End_P,Bulk_Comp0,CMF,Tp_min,Tp_inc,Tp_max,Iso_mode,KD,T_continuous,plotit)

Key results (final melt and residue compositions) are printed as text files. Detailed results can be accessed in the structures detail_comp and detail_comp2 (the latter only save results when melting has started)

To run the model for the first time use
- example_MAGMARS.m (reproduces elements of figure 2a and 6 from the main manuscript)

Alternatively use
- run_MAGMARS.m to melt a Dreibus and Wänke 1985 mantle composition at different temperatures

-----------------------------------------------------------------------------------
(2) Thermobarometer 

Open and copy and past the composition of primary basalts for which you want to estimate the P-T conditions (assuming batch melting) 
Each line is a composition (with 11 columns SiO2 TiO2 Al2O3 Cr2O3 FeO MnO MgO CaO Na2O K2O P2O5)

Printout and save (thermobarometer.txt) the following thermobarometer results: 
% (1) recommended P-independant thermometer (this study)
% (2) recommended barometer (this study, Lee et al. 2009 recal)
% (3) MAGMARS harzburgite melting thermometer (P dependant, this study)
% (4) thermometer eq. 15 from Putirka 2008
% (5) oliv-liq thermometer AB from Putirka 2005 
% (6) oliv-liq thermometer AB, recalibrated (this study)
% (7) Barometer from Lee et al. 2009

-----------------------------------------------------------------------------------
(3) Inversion routine subfolder

The subfolder [inversion] contains 2 scripts to run MAGMARS while randomly varying the input parameters around an average value (RandomSearch_MM.m) and then comparing the generated database to a target primary melt composition to see under which conditions and from which mantle source it could derive (MatchMelt_MM.m). These scripts were used to generate Table 3 in the main manuscript but note that this is an iterative process that has to be guided by the user.

-----------------------------------------------------------------------------------
(4) MAGMARS_database.zip

Detail of the database used to parametrize MAGMARS 

(5) C2021_ExpData.zip

Electron microprobe analyses for the experiments of Collinet et al. 2021 JGR:P

-----------------------------------------------------------------------------------
(6) Collinet_etal_2023_GRL_SI.zip

Table S1-S4 and main supporting information for Collinet et al. (2023, submitted to GRL)

(7) Fastball_source_random_search.zip

Inversion routine to constrain the source of the Gusev basalt Fastball (Collinet et al., 2023, submitted to GRL)

(8) GRS_volcanic_provinces.zip

MAGMARS results used in figure 3 of Collinet et al. (2023, submitted to GRL) to match the GRS volcanic provinces of Baratoux et al. 2011 with 3 different primitive mantle compositions.


