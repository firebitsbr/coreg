# MATLAB/Fieldtrip Yokogawa Coregistration Scripts

## 1. realign_MEG_sensors folder

This folder outlines how to realign the MEG sensors based on the position of the 5 marker coils (instead of doing this using the MEG160 Yokogawa software).

## 2. coreg_yokogawa_icp

This is a work in progress script to improve the coregistation between structural MRI and MEG data with polhemus headshape data. This approach uses the iterative closest point (ICP) algorithm to match scalp surface with downsampled headshape information.

The function currently works well for data acquired with FACIAL INFORMATION (eyes and nose). If you don't have this the function probably won't improve manual coreg (marking the 3 fiducials by hand) and may even reduce accuracy. More comprehensive testing is needed to make the code stable for release.

## coreg_yokogawa_icp_adjust_weights.m 

This is currently the most up to date script. The function allows you to weight facial points higher when performing the ICP fit. It seems to work well with a weighting factor of 0.5-0.8. This function also has the option of taking out a bad coil (see function comments).

### Please download CaptureFigVid for "cool" animations

```matlab
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
%
% coreg_yokogawa_icp_adjust_weights is a function to coregister a structural 
% MRI with MEG data and associated headshape information
%
% Written by Robert Seymour Oct 2017 - Feb 2018 (some subfunctions 
% contributed by Paul Sowman)
%
% INPUTS:
% - dir_name        = directory name for the output of your coreg
% - confile         = full path to the con file
% - mrkfile         = full path to the mrk file
% - mri_file        = full path to the NIFTI structural MRI file
% - hspfile         = full path to the hsp (polhemus headshape) file
% - elpfile         = full path to the elp file
% - hsp_points      = number of points for downsampling the headshape (try 100-200)
% - scalpthreshold  = threshold for scalp extraction (try 0.05 if unsure)
%
% VARIABLE INPUTS (if using please specify all):
% - do_vids         = save videos to file. Requires CaptureFigVid.
% - weight_number   = how strongly do you want to weight the facial points?
% - bad_coil        = is there a bad coil to take out?
%
% EXAMPLE FUNCTION CALL:
% coreg_yokogawa_icp_adjust_weights(dir_name,confile,mrkfile,mri_file,...
% hspfile,elpfile,hsp_points, scalpthreshold,'yes',0.8,'')
%
% OUTPUTS:
% - grad_trans              = correctly aligned sensor layout
% - headshape_downsampled   = downsampled headshape (original variable name I know)
% - mri_realigned           = the mri realigned based on fiducial points
% - trans_matrix            = transformation matrix for accurate coregistration
% - mri_realigned2          = the coregistered mri based on ICP algorithm
% - headmodel_singleshell   = coregistered singleshell headmodel
%
% THIS IS A WORK IN PROGRESS FUNCTION - any updates or suggestions would be
% much appreciated
%
%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%%
```

![Imgur](https://i.imgur.com/UDnlAqA.png)

## Papers:

- [Gohel, B., Lim, S., Kim, M. Y., Kwon, H., & Kim, K. (2017). Approximate Subject Specific Pseudo MRI from an Available MRI Dataset for MEG Source Imaging. Frontiers in neuroinformatics, 11, 50.](https://www.frontiersin.org/articles/10.3389/fninf.2017.00050/full)
 
- [Whalen, C., Maclin, E. L., Fabiani, M., & Gratton, G. (2008). Validation of a method for coregistering scalp recording locations with 3D structural MR images. Human Brain Mapping, 29(11), 1288-1301.](http://onlinelibrary.wiley.com/doi/10.1002/hbm.20465/full)



