# Country Report

Hope Country Report (HCR) is a pivotal component within the Hope platform, specifically designed to empower UNICEF country offices with the ability to generate customized reports tailored to their unique requirements. These reports are not mere static compilations of data, but rather dynamic representations of information extracted from the Hope Database.

At the core of this data retrieval process lies the utilization of Python and Django code. These programming languages provide the necessary tools to extract and manipulate data from the database, enabling the creation of reports that are both informative and visually appealing.

To gain a comprehensive understanding of the available data within the Hope Database, it is essential to refer to the GitHub repository at this


## Features


## Repository

<https://github.com/unicef/hope-country-report>


### Glossary

<report:Parametrizer/Argument>

Dataset : Dictionary used to create reports

System flagged are special arguments with related sync

Power Query
It's a read only query to be executed on database, it generate a dataset.

target: is the model from which the query starts from

parametrizer

active

daily refreshed

code:
result variable contains the result
extra variable contains extra context 

Formatter
template to display or export reports

content type

code

Dataset
Dataset

has reference to query used

Report
Report connecting Query, Dataset, and Formatter

Document Report
is an instance obtained enumerating a Report for each Argument combination.

access is granted based on:

Business Area as per User Group -> PowerQuery Viewer

limited_access to field
