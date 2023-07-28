# Structural modeling of Multispecies Fisheries

This is the code used to run the economic simulations for:
Birkenbach, Lee, and Smith "Counterfactual Modeling of Multispecies Fisheries Outcomes Under Market-Based Regulation."  Journal of the Association of Environmental and Resource Economists. 

[![DOI](https://zenodo.org/badge/479089401.svg)](https://zenodo.org/badge/latestdoi/479089401)




This economic simulation are intended to be integrated into [a bioeconomic model of groundfish](https://github.com/lkerr/groundfish-MSE).  However, to focus on the counterfactual vs status-quota simulations, we have removed most of the biological and ecosystem machinery.

This was:
1.  Deforked this from https://github.com/lkerr/groundfish-MSE/commit/6af544af12d541102bdd2253931f054dd06709c8
2.  Only the Econ_Only2 branch was retained. It was renamed to main. 
3.  All of the superfluous non-economic bits were removed from this branch. If I have deleted too many, I should go here:

[https://github.com/mle2718/READ-SSB-Lee-Countefactual_Modeling_of_Multispecies_Fisheries/commit/6af544af12d541102bdd2253931f054dd06709c8](https://github.com/mle2718/READ-SSB-Lee-Counterfactual_Modeling_of_Multispecies_Fisheries/tree/6af544af12d541102bdd2253931f054dd06709c8)
and restore what is needed.


# Replication Overview and Setup
Replicating the simulations will take a few steps.
1. Clone this repository. Choice Model results (Tables 3 and A6) and Harvest Regression model results (Tables A4 and A5) are contained in ``/data/data_raw/econ``.  Note that the choice model coefficients contained in ``/data/data_raw/econ`` are the *raw* coefficients and must be exponentiated to compare them to Tables 3 and A6 in the manuscript.   
2. Obtain the simulation data. The simulation data should be placed into the ``/data/data_raw/econ`` folder.
3. Set up the data. Run the following 3 stata do files and 2 R scripts that are in the ``/preprocessing/economic`` directory:
   1.  ``/preprocessing/economic/wrapper_common.do``
   2.  ``/preprocessing/economic/wrapper_validation.do``
   3.  ``/preprocessing/economic/wrapper_CF.do``
   4.  ``/preprocessing/economic/pre_process_econ_AB_counterfactual.R``
   5.  ``/preprocessing/economic/pre_process_econ_AB_validation.R``


Different types of simulations are run by passing different parameters into the model using the various  ``mprocEcon_XXX.csv`` files.
 
# Validation (Catch Share) simulations
To run the validation (CS) simulation, ensure that line 18 in  ``/modelParameters/set_om_parameters_global.R`` is:
```
mprocfile<-"mprocEcon_validate.csv"
```

Then, run  ``/processes/runSim_Econonly_validation.R.``  Model results in the manuscript correspond to the output data where ``m==2`` (see the file ``/modelParameters/mprocEcon_validate.csv``).  These data are used for:
1.  The 75th and 25th percentile CS Range and Predicted CS line in Figures 1-4 and Figures 8-9 
2.  The predicted (CS) line in Figure 5
3.  Figures 6,7,10,11, A1, and A2 in combination with the Counterfactual (DAS) Simulations  

There are three other models that are robustness checks.  

# Counterfactual Simulations 
To run the Countefactual (DAS) simulations, change line 18 in  ``/modelParameters/set_om_parameters_global.R`` to read:
```
mprocfile<-"mprocEcon_counterfactual_closemult.csv"
```
Then, run  ``/processes/runSim_Econonly_counterfactual_closemult.R.``  Model results in the manuscript correspond to the output data where ``m==2`` (see the file ``/modelParameters/mprocEcon_validate.csv``).  These data are used for:
1.  The 75th and 25th percentile DAS Range and Predicted DAS line in Figures 3-4 and Figures 8-9 
2.  The predicted (DAS) line in Figure 5
3.  Figures 6,7,10,11, A1, and A2 in combination with the CS Simulations  

# Counterfactual Simulations V2
We also simulated the models under regulatory scenario in which reaching the catch limit for stock A *does not* result in cessation of fishing for other stocks caught along with stock A.  This is a bit unrealistic.  If you want to run this type of model, change line 18 in  ``/modelParameters/set_om_parameters_global.R`` to read:
```
mprocfile<-"mprocEcon_counterfactual_single.csv"
```

Then, run  ``/processes/runSim_Econonly_counterfactual_closesingle.R.`` 


# Disclaimer
“This repository is a scientific product and is not official communication of the National Oceanic and Atmospheric Administration, or the United States Department of Commerce. All NOAA GitHub project code is provided on an ‘as is’ basis and the user assumes responsibility for its use. Any claims against the Department of Commerce or Department of Commerce bureaus stemming from the use of this GitHub project will be governed by all applicable Federal law. Any reference to specific commercial products, processes, or services by service mark, trademark, manufacturer, or otherwise, does not constitute or imply their endorsement, recommendation or favoring by the Department of Commerce. The Department of Commerce seal and logo, or the seal and logo of a DOC bureau, shall not be used in any manner to imply endorsement of any commercial product or activity by DOC or the United States Government.”



Who worked on this project - Lee, Birkenbach, Smith

When this project was created - Started in 2015. Live in July 2023

What the project does - This is code to replicate the simulations in Birkenbach, Lee, and Smith "Counterfactual Modeling of Multispecies Fisheries Outcomes Under Market-Based Regulation."  Journal of the Association of Environmental and Resource Economists. 

Why the project is useful - See previous.

How users can get started with the project - Clone, obtain data from authors.

Where users can get help with your project - Open an issue.

maintains and contributes to the project - Lee
