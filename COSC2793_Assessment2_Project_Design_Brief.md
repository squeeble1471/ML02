# COSC2793 Assessment 2 --- Machine Learning Modelling

## Project Design Brief & Working Specification

**Course:** COSC2793 Computation Machine Learning\
**Assessment:** Assessment 2 --- Machine Learning Modelling\
**Weight:** 40%\
**Due:** Sunday, 4 October 2026, 11:59 PM AEDT (Week 10)\
**Task type:** Individual\
**Current project stage:** End of Week 8 / entering Week 9

------------------------------------------------------------------------

# 1. Project Goal

Develop, evaluate, compare, and justify machine learning models that
predict the **fire intensity level** of a wildfire event from
environmental, geographic, temporal, and satellite-observation features.

This is a **four-class classification problem**.

Target variable:

-   `fire_intensity`
-   `0` = Low
-   `1` = Moderate
-   `2` = High
-   `3` = Extreme

The final system must train on the supplied training dataset and produce
predictions for the supplied test dataset.

Only techniques taught in class up to and including **Week 8** may be
used.

------------------------------------------------------------------------

# 2. Core Research Question

> How effectively can Decision Tree, Support Vector Machine, and Neural
> Network models classify wildfire intensity into four levels using the
> supplied environmental and observational data?

The project should not simply determine which model has the highest
score. It should investigate:

-   how each model behaves;
-   how hyperparameters affect training and validation performance;
-   whether models underfit or overfit;
-   model stability and convergence;
-   differences in model complexity;
-   suitability of each model for this dataset;
-   trade-offs involved in selecting the final model.

------------------------------------------------------------------------

# 3. Dataset

## 3.1 Files

Training data:

`wildfire_cls_train_full.csv`

Test data:

`wildfire_cls_test_features.csv`

The training dataset contains the target variable. The test dataset does
not.

The data covers:

-   7 regions;
-   35 countries;
-   environmental conditions;
-   geographic information;
-   temporal information;
-   satellite-derived observations.

The assessment states that these regions and countries represent the
intended deployment domain. Generalisation to unseen countries or
regions does not need to be investigated.

## 3.2 Features

### Geographic

-   `latitude`
-   `longitude`
-   `region`
-   `country`

### Temporal

-   `acq_date`
-   `acq_time`
-   `year`
-   `month`
-   `season`
-   `daynight`

### Fire / Observation

-   `fire_type`
-   `satellite`
-   `instrument`
-   `brightness_k`
-   `confidence`

### Weather / Environmental

-   `temp_max_c`
-   `wind_max_kmh`
-   `precip_mm`
-   `humidity_pct`

### Target

-   `fire_intensity`

------------------------------------------------------------------------

# 4. Required Models

Exactly the following three model families must be developed and
compared:

1.  **Decision Tree**
2.  **Support Vector Machine (SVM)**
3.  **Neural Network**

All three require controlled hyperparameter experiments rather than a
single arbitrary configuration.

Because this is **COSC2793**, at least one additional hyperparameter
beyond the specifically required parameter(s) must be investigated for
each model.

------------------------------------------------------------------------

# 5. Evaluation Design

A consistent evaluation framework must be used across the models.

## 5.1 Data Separation

The supplied test dataset must remain separate from model development.

The training dataset will be divided into:

-   training data;
-   validation data.

Possible permitted approach:

-   hold-out validation; **or**
-   k-fold cross-validation.

**Chosen approach:**\
*TODO: record final choice and justification.*

## 5.2 Metrics

Required/appropriate metrics include:

-   Accuracy
-   F1-score

The same principal metrics should be used across all three models so
that comparisons are meaningful.

**F1 averaging method:**\
*TODO: determine and justify based on the four-class task/class
distribution.*

## 5.3 Experimental Principle

Change hyperparameters systematically and record:

-   parameter values;
-   training performance;
-   validation performance;
-   relevant plots;
-   observations;
-   evidence of underfitting/overfitting;
-   stability/sensitivity;
-   theoretical explanation where appropriate.

Do not select hyperparameters using the final test dataset.

------------------------------------------------------------------------

# 6. Proposed Notebook Architecture

The notebook should be organised so that it can also act as an auditable
record of the entire ML workflow.

## 0. Setup

-   Imports
-   Random seed(s)
-   Configuration/constants
-   File paths
-   Reproducibility information

## 1. Load Data

-   Load training CSV
-   Load test CSV
-   Confirm shapes
-   Display representative rows
-   Verify target exists only in training data
-   Verify train/test feature compatibility

## 2. Dataset Inspection

Investigate:

-   dimensions;
-   column names;
-   data types;
-   categorical vs numerical features;
-   missing values;
-   duplicate rows if relevant;
-   target class distribution;
-   unusual or invalid values;
-   ranges of numerical variables.

Record observations in Markdown as the investigation proceeds.

## 3. Exploratory Data Analysis

Investigate relationships including:

-   feature distributions;
-   target distribution;
-   relationships between numerical features;
-   relationships between features and `fire_intensity`;
-   categorical feature distributions;
-   potentially redundant features;
-   possible feature importance/relevance;
-   possible data quality issues.

Questions to answer:

-   How are features related to one another?
-   How are features related to the target?
-   Are all features useful?
-   Are any variables redundant?
-   Are classes balanced?
-   Are missing values systematic?
-   Are there features that require transformation or encoding?

## 4. Preprocessing

Design a reproducible preprocessing workflow.

### Missing Values

Investigate:

-   which columns contain missing values;
-   quantity/proportion missing;
-   suitable treatment for numerical features;
-   suitable treatment for categorical features.

**Chosen strategy:**\
*TODO*

**Justification:**\
*TODO*

### Categorical Encoding

Identify categorical columns and encode them using techniques taught by
Week 8.

**Chosen strategy:**\
*TODO*

### Numerical Features

Determine whether numerical scaling is required.

Scaling is particularly relevant to models such as SVM and Neural
Networks.

**Chosen strategy:**\
*TODO*

### Feature Processing

Consider whether supplied fields contain redundant representations,
particularly temporal variables such as:

-   `acq_date`
-   `year`
-   `month`

Any feature removal or transformation must be justified rather than
performed arbitrarily.

## 5. Evaluation Framework

Implement the chosen training/validation procedure.

Requirements:

-   reproducible split/folds;
-   no test-data leakage;
-   preprocessing fitted appropriately;
-   consistent metrics;
-   consistent comparison framework.

------------------------------------------------------------------------

# 7. Decision Tree Design

## Objective

Establish an interpretable baseline and investigate the relationship
between tree complexity and generalisation.

## Required Experiments

Investigate:

-   `max_depth`

Also investigate at least one additional hyperparameter for COSC2793.

**Additional parameter:**\
*TODO*

Possible experiment structure:

  -----------------------------------------------------------------------------------
  Experiment     max_depth Additional         Train   Validation          F1 Notes
                           Parameter       Accuracy     Accuracy             
  ------------ ----------- ------------ ----------- ------------ ----------- --------
  DT-01                                                                      

  DT-02                                                                      

  DT-03                                                                      
  -----------------------------------------------------------------------------------

## Required Analysis

Answer:

-   How does `max_depth` affect performance?
-   At what point does additional complexity stop improving validation
    performance?
-   Is there evidence of underfitting?
-   Is there evidence of overfitting?
-   How would limiting depth/post-pruning affect performance?
-   What can be learned from the resulting tree structure?

## Required Visualisation

-   Performance vs model complexity
-   Visualisation of the obtained tree structure

**Best validation configuration:**\
*TODO*

------------------------------------------------------------------------

# 8. SVM Design

## Objective

Investigate how different decision-boundary assumptions and
regularisation affect classification performance.

## Required Experiments

Compare:

-   Linear kernel
-   RBF kernel

Investigate:

-   `C`
-   at least one additional hyperparameter for COSC2793

**Additional parameter:**\
*TODO*

For an RBF SVM, a relevant parameter may be investigated if it has been
taught in the course.

Example experiment table:

  ----------------------------------------------------------------------------------------
  Experiment   Kernel            C Additional        Train   Validation         F1 Notes
                                   Parameter      Accuracy     Accuracy            
  ------------ -------- ---------- ------------ ---------- ------------ ---------- -------
  SVM-01       linear                                                              

  SVM-02       RBF                                                                 

  SVM-03       RBF                                                                 
  ----------------------------------------------------------------------------------------

## Required Analysis

Answer:

-   How does linear SVM performance compare with RBF?
-   How does `C` affect training performance?
-   How does `C` affect validation performance?
-   Is the model sensitive to the selected hyperparameters?
-   How does the additional hyperparameter affect the decision boundary?
-   Is there evidence of underfitting or overfitting?

**Best validation configuration:**\
*TODO*

------------------------------------------------------------------------

# 9. Neural Network Design

## Objective

Investigate optimisation behaviour, convergence, model capacity, and
generalisation.

## Required Experiments

Investigate multiple:

-   learning rates

Also investigate at least one additional hyperparameter for COSC2793.

**Additional parameter:**\
*TODO*

Example experiment table:

  ----------------------------------------------------------------------------------------
  Experiment      Learning Additional         Train   Validation          F1 Convergence
                      Rate Parameter       Accuracy     Accuracy             Notes
  ------------ ----------- ------------ ----------- ------------ ----------- -------------
  NN-01                                                                      

  NN-02                                                                      

  NN-03                                                                      
  ----------------------------------------------------------------------------------------

## Required Visualisations

-   Training loss across epochs
-   Performance comparison across learning rates
-   Other useful training/validation curves where appropriate

## Required Analysis

Answer:

-   How does learning rate affect training behaviour?
-   Which learning rates converge?
-   Which learning rate produces the most stable convergence?
-   Are any rates too small or too large?
-   What do the loss curves reveal?
-   Does the network overfit?
-   How does the additional hyperparameter affect performance?

**Best validation configuration:**\
*TODO*

------------------------------------------------------------------------

# 10. Model Comparison

After individual model experiments are complete, compare the best
justified configuration of each model.

Suggested summary table:

  ----------------------------------------------------------------------------------------
  Model          Accuracy           F1 Stability   Complexity   Hyperparameter   Notes
                                                                Sensitivity      
  ---------- ------------ ------------ ----------- ------------ ---------------- ---------
  Decision                                                                       
  Tree                                                                           

  SVM                                                                            

  Neural                                                                         
  Network                                                                        
  ----------------------------------------------------------------------------------------

Questions to answer:

-   Which model performs best under the evaluation framework?
-   How do the models differ in how they separate classes?
-   Which produces simpler or more complex boundaries?
-   Which models are most sensitive to hyperparameters?
-   Which models appear most stable?
-   Do more complex models actually perform better?
-   Do the experimental results agree with theoretical expectations?
-   If results differ from expectations, why might that have happened?

------------------------------------------------------------------------

# 11. Final Model Selection

The final model must be selected using evidence from the validation
experiments.

Selection must consider more than raw performance.

Possible considerations:

-   Accuracy
-   F1-score
-   Generalisation
-   Train/validation gap
-   Stability
-   Hyperparameter sensitivity
-   Model complexity
-   Interpretability
-   Computational requirements
-   Suitability for the wildfire classification problem

**Selected model:**\
*TODO*

**Selected configuration:**\
*TODO*

**Justification:**\
*TODO*

------------------------------------------------------------------------

# 12. Final Test Prediction

Only after the final model and configuration have been selected:

1.  Prepare the supplied test features using the final preprocessing
    procedure.
2.  Generate predictions using the selected model.
3.  Preserve the original test-row order.
4.  Convert predictions to the required label names:
    -   `Low`
    -   `Moderate`
    -   `High`
    -   `Extreme`
5.  Save the predictions as:

`{student_number}_predictions.csv`

The CSV must contain exactly one column:

`fire_intensity`

Do not include the DataFrame index.

------------------------------------------------------------------------

# 13. Final Deliverables

Submission requires a ZIP plus a separately submitted report PDF.

The ZIP must contain:

-   Jupyter notebook (`.ipynb`)
-   PDF export of the notebook
-   prediction CSV
-   report PDF

The report PDF is therefore submitted:

-   inside the ZIP; and
-   separately.

For COSC2793, the report must be **10--20 pages**, including figures,
tables, references, appendices, etc.

------------------------------------------------------------------------

# 14. Report Structure

## 0. Introduction

Briefly establish:

-   wildfire intensity classification problem;
-   purpose of the project;
-   ML approach;
-   overall workflow.

## A. Task Definition and Dataset Description

Cover:

-   classification task;
-   prediction target;
-   four classes;
-   dataset structure;
-   feature categories;
-   important characteristics;
-   potential challenges.

## B. Exploratory Data Analysis and Data Handling

Cover:

-   distributions;
-   target balance;
-   missing data;
-   feature relationships;
-   feature-target relationships;
-   preprocessing;
-   encoding;
-   scaling;
-   data splitting;
-   justification for decisions.

## C. Model Development and Performance Analysis

### Decision Tree

-   rationale;
-   advantages/disadvantages;
-   hyperparameter experiments;
-   quantitative results;
-   visualisations;
-   tree structure;
-   underfitting/overfitting;
-   theoretical interpretation.

### SVM

-   rationale;
-   advantages/disadvantages;
-   linear vs RBF;
-   `C` experiments;
-   additional COSC2793 hyperparameter;
-   quantitative results;
-   visualisations;
-   behaviour and sensitivity.

### Neural Network

-   rationale;
-   advantages/disadvantages;
-   learning-rate experiments;
-   additional COSC2793 hyperparameter;
-   loss curves;
-   convergence;
-   quantitative results;
-   model behaviour.

## D. Model Comparison

Compare all three models using the same evaluation framework.

Discuss:

-   performance;
-   complexity;
-   stability;
-   sensitivity;
-   generalisation;
-   theoretical expectations.

## E. Final Model Selection, Justification and Evaluation

Explain:

-   selected model;
-   selected hyperparameters;
-   why it was selected;
-   evidence supporting selection;
-   considerations beyond raw performance;
-   final prediction procedure.

## F. Ethical Considerations and Professional Responsibilities

Potential areas to investigate:

-   consequences of underestimating wildfire intensity;
-   consequences of overestimating wildfire intensity;
-   geographic/data representation;
-   limitations of historical observations;
-   reliability and uncertainty;
-   responsible interpretation of automated predictions;
-   appropriate human oversight.

Only claims supported by the dataset, experiments, course material, or
cited literature should be made.

## G. Conclusion

Summarise:

-   task;
-   major experimental findings;
-   model comparison;
-   final selection;
-   limitations.

## H. References

Use the required referencing style consistently.

------------------------------------------------------------------------

# 15. Assessment Weighting

  Component                                          Weight
  ----------------------------------------------- ---------
  Task and Dataset Understanding                         5%
  EDA and Data Handling                                  5%
  Model Development and In-depth Analysis           **40%**
  Model Comparison, Selection and Justification         10%
  Prediction of Test Data                               10%
  Report Quality                                    **30%**

## Priority Implication

The majority of marks are concentrated in:

1.  systematic model experiments and analysis;
2.  clear interpretation of model behaviour;
3.  high-quality reporting.

The project should therefore prioritise **understanding and explaining
experiments**, rather than simply obtaining the highest possible
validation score.

------------------------------------------------------------------------

# 16. Project Timeline

## Week 7 --- Foundation

-   [ ] Review full specification
-   [ ] Download datasets
-   [ ] Load datasets
-   [ ] Inspect dataset structure
-   [ ] Initial EDA
-   [ ] Investigate missing values
-   [ ] Investigate class distribution
-   [ ] Design preprocessing
-   [ ] Implement basic preprocessing

## Week 8 --- Model Development

-   [ ] Establish evaluation framework
-   [ ] Implement Decision Tree baseline
-   [ ] Evaluate Decision Tree
-   [ ] Run Decision Tree hyperparameter experiments
-   [ ] Implement SVM
-   [ ] Compare linear and RBF kernels
-   [ ] Run SVM hyperparameter experiments
-   [ ] Implement Neural Network
-   [ ] Run learning-rate experiments
-   [ ] Run additional NN hyperparameter experiment
-   [ ] Produce loss curves
-   [ ] Record all results

### End-of-Week-8 Milestone

**All three models should run successfully and the principal
hyperparameter experiments should be complete.**

------------------------------------------------------------------------

## Week 9 --- Analysis and Final Pipeline

-   [ ] Consolidate experimental results
-   [ ] Produce clean comparison tables
-   [ ] Produce final plots
-   [ ] Analyse underfitting/overfitting
-   [ ] Analyse hyperparameter sensitivity
-   [ ] Compare model behaviour
-   [ ] Relate results to theory
-   [ ] Select final model
-   [ ] Finalise preprocessing pipeline
-   [ ] Finalise selected model configuration
-   [ ] Begin writing report sections using completed experimental
    results

------------------------------------------------------------------------

## Week 10 --- Finalisation

-   [ ] Train/finalise selected model as appropriate
-   [ ] Generate test predictions
-   [ ] Verify prediction labels
-   [ ] Verify prediction row count/order
-   [ ] Export prediction CSV
-   [ ] Complete report
-   [ ] Check report against rubric
-   [ ] Clean notebook
-   [ ] Add run instructions
-   [ ] Restart/run notebook from beginning to verify reproducibility
-   [ ] Export notebook to PDF
-   [ ] Assemble ZIP
-   [ ] Verify all submission files
-   [ ] Submit before Sunday 4 October, 11:59 PM AEDT

------------------------------------------------------------------------

# 17. Experiment Log

Use this section to record experiments immediately rather than trying to
reconstruct them later.

## Decision Tree

### DT-01

**Configuration:**\
*TODO*

**Results:**\
*TODO*

**Observation:**\
*TODO*

**Interpretation:**\
*TODO*

------------------------------------------------------------------------

## SVM

### SVM-01

**Configuration:**\
*TODO*

**Results:**\
*TODO*

**Observation:**\
*TODO*

**Interpretation:**\
*TODO*

------------------------------------------------------------------------

## Neural Network

### NN-01

**Configuration:**\
*TODO*

**Results:**\
*TODO*

**Observation:**\
*TODO*

**Interpretation:**\
*TODO*

------------------------------------------------------------------------

# 18. Decisions Log

Record important design decisions and the evidence supporting them.

  Decision                       Choice   Reason / Evidence
  ------------------------------ -------- -------------------
  Validation strategy            TODO     
  Missing numerical values       TODO     
  Missing categorical values     TODO     
  Categorical encoding           TODO     
  Numerical scaling              TODO     
  Features removed               TODO     
  Decision Tree configuration    TODO     
  SVM configuration              TODO     
  Neural Network configuration   TODO     
  Final model                    TODO     

------------------------------------------------------------------------

# 19. Questions / Issues

Keep unresolved questions here so they do not disappear during
implementation.

-   [ ] What validation method will be used?
-   [ ] Which F1 averaging method is appropriate?
-   [ ] Which columns contain missing data?
-   [ ] Which categorical encoding method is permitted/appropriate?
-   [ ] Which features require scaling?
-   [ ] Are any supplied features redundant?
-   [ ] Which additional Decision Tree hyperparameter will be
    investigated?
-   [ ] Which additional SVM hyperparameter will be investigated?
-   [ ] Which additional Neural Network hyperparameter will be
    investigated?
-   [ ] How will experiment results be stored consistently?
-   [ ] Which plots will be included in the final report?

------------------------------------------------------------------------

# 20. Reproducibility Checklist

Before submission:

-   [ ] Random seeds are explicitly set where applicable.
-   [ ] Notebook runs from top to bottom without relying on hidden
    state.
-   [ ] Required packages/imports are documented.
-   [ ] File paths are portable/relative where possible.
-   [ ] Training and validation procedures are reproducible.
-   [ ] Test data is not used for hyperparameter selection.
-   [ ] Preprocessing is consistently applied.
-   [ ] All figures have readable labels/titles.
-   [ ] Tables clearly identify metrics and configurations.
-   [ ] Final CSV has the correct column name.
-   [ ] Final CSV contains label names rather than incorrect numeric
    output.
-   [ ] Final CSV preserves test sample order.
-   [ ] Notebook and notebook PDF are identical in content.
-   [ ] Report is within the COSC2793 10--20 page requirement.

------------------------------------------------------------------------

# 21. GenAI Usage Log

The assessment permits GenAI use, but use must be declared and
prompts/use cases documented.

Record assistance as it occurs.

  ---------------------------------------------------------------------------------
  Date           Tool           Purpose        Prompt /        How Output Was Used
                                               Description     
  -------------- -------------- -------------- --------------- --------------------
  2026-09-19     ChatGPT        Project        Created a       Used as
                                planning       design          project-management
                                               brief/work plan documentation;
                                               from the        implementation and
                                               supplied        analysis to be
                                               assessment      completed and
                                               specification   verified by student

                                                               
  ---------------------------------------------------------------------------------

Do not submit generated material without understanding, checking, and
adapting it. All submitted code, analysis, results, and claims remain
the student's responsibility.

------------------------------------------------------------------------

# 22. Definition of Done

The project is complete when:

-   all three required models have been implemented;
-   required and COSC2793-specific hyperparameter experiments have been
    completed;
-   experiments use a consistent evaluation framework;
-   model behaviour has been analysed rather than merely reported;
-   the final model has been selected and justified;
-   test predictions have been generated in the exact required format;
-   the notebook is reproducible;
-   the notebook PDF matches the notebook;
-   the report addresses every required section and model-specific
    question;
-   GenAI use has been acknowledged as required;
-   all files have been checked against the submission specification and
    rubric.
