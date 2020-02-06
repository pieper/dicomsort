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

```
% dicomsort.py --help
dicomsort [options...] sourceDir targetDir/<patterns>

 where [options...] can be:
    [-z,--compressTargets] - create a .zip file in the target directory
    [-d,--deleteSource] - remove source files/directories after sorting
    [-f,--forceDelete] - remove source without confirmation
    [-k,--keepGoing] - report but ignore dupicate target files
    [-v,--verbose] - print diagnostics while processing
    [-s,--symlink] - create a symlink to dicom files in sourceDir instead of copying them
    [-t,--test] - run the built in self test (requires internet)
    [-u,--unsafe] - do not replace unsafe characters with '_' in the path
    [--help] - print this message

 where sourceDir is directory to be scanned or "" (null string) to read file list from stdin

 where targetDir/<patterns...> is a string defining the output file and directory
 names based on the dicom tags in the file.

If patterns are not specified, the following default is used:
 
  %PatientName-%Modality%StudyID-%StudyDescription-%StudyDate/%SeriesNumber_%SeriesDescription-%InstanceNumber.dcm

Example 1:

  dicomsort data sorted/%PatientName/%StudyDate/%SeriesDescription-%InstanceNumber.dcm

  could create a folder structure like:

  sorted/JohnDoe/2013-40-18/FLAIR-2.dcm

Example 2:

  find DicomSourceDir/ | grep "IMA$" | dicomsort -s "" DicomTargetDir

  would scan DicomSourceDir for file pathnames ending in IMA and create an
  output directory DicomTargetDir. The folder structure will be created using
  the default pattern with symbolic links to the source dicom data files.
```

Requires
========
Python 2.x or 3.x

pydicom
