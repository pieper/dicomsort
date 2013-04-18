dicomsort
=========

A project to provide custom sorting and renaming of dicom files


Description
-----------

Given DICOM files in a random folder structure, this program copies all into a user-defined folder hierarchy, creating folders as necessary and changing DICOM file names to be more meaningful.

The user can define the target folder structure and file naming by using a string consisting of concatenated tag names (like 'PatientName'), underscores and slashes.
The last part of the string (as separated by slashes) denotes the naming convention for the file parts.

An Example: a target string of 
 'Modality/PatientName_PatientID' 
means that all DICOM images are arranged in a base folder and named by PatientName_PatientID, 
followed by an underscore and a unique number for every file that falls into the same category (and is not the same..?)

dicomsort returns with a count for both DICOM files organized and non-DICOM (or invalid DICOM) files skipped.
It aborts with an error if it is to overwrite any existing file.


Usage
-----

    dicomsort.py -s(?) "tag1_tag2/tag3/tag4_tag5"  [-z] src_folderroot tgt_folderroot



This would recursively copy all files found in the folder `src_folderroot` into a hierarchy of `tgt_folderroot/tag1_tag2/tag3/tag4_tag5_UNIQUEFILENUMBER`
