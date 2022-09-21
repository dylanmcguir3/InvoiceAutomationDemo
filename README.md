# Project Structure

Project Layout for Invoice Processor App. From start to finish the application takes a PDF invoice from a email inbox, locates the data, highlights it on the page, and stores it in a csv. If no error is detected in the processor, than the PDF is output along with the data. If an error is detected, then the PDf goes to the GUI with the data to be reviewed by humans. Inside the GUI there is a variety of features to aid the user in resolving uncertainties such as intelligent lookups for vendors and customers and their addresses. When documents are finished being reviewed in the gui they go to the same output location as the invoices where no error was detected in the same format.

# File Processor/Manager

## monitor_directory.py
File that makes calls to processor on any invoices that come into a directory and sorts them by vendor name \
**INPUT:** directory (specified by config)\
**OUTPUT:** outputs a folder of invoices split into sub-directories based on letter groups specifed in config \
each sub directory contains 100 invoices with highlighted data and a data csv
**Dependencies:** process.py

## process.py
Processor that uses data returned by the extraction algorithm to store the transactional data and highlight its position the pdf invoices
**INPUT:** invoice pdf\
**OUTPUT:** outputs a single pdf to a folder based on vendor name and writes a row 
to the csv in that folder\
**Dependancies:** extract.py,

## extract.py
Algorithm that extracts data from pdf
**Dependancies:** template_specific_checks.py
**INPUT:** batch of invoices and csv data\
**OUTPUT:** relevant data fields in correct file format and pdfs without highlights

## split.py
Infastructure and logic for splitting a pdf


# GUI


## gui_main.py
Call to the HumanReviewGUI class, for reviewing invoices kicked out by the processor\
**INPUT:** batch of invoices and csv data\
**OUTPUT:** relevant data fields in correct file format and pdfs without highlights

## gui_elements.py 
Stores subclasses and style elements for the GUI 

## lookups.py
Infastructure for the intelligent lookup algorithms

# Global

## constants.py
Stores  global constants for both the GUI and the processor

## logger.py 
Houses the logging object and its methods

## settings.py
Settings class contains settings for the user to configure in the GUI and the save state for the application

# Helper
Various classes that support the function of processes in the GUI and processor

## kickstart.py
File that contains functions called by the GUI that kick off processes in the backend

## connectionObj
File that contains connection to databases and helper methods

## csvObj
csvObj used for extracting data from an excel document

## azureObj
File that contains azureObj which interacts with the Azure Intelligent Document\
Processing API, used when AI extracts info instead of template


## Template

## MakeTemplateGUI
File that contains code for a basic gui that allows users to highlight label-data pairs and extracts\
necessary information to create a new document template to put in the database

## template.py
Contains a template object specified by template in the database, and carries out pre and post processing
