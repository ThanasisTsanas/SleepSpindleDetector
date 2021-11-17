# SleepSpindleDetector
Detect sleep spindles from EEG signals (single-lead EEG, no hypnogram required)

I have purposefully created my function to be easy to use out-of-the box: simply provide the EEG data and the sampling frequency, and you will obtain estimates of the spindles in the EEG signal in terms of the actual samples.

**The two algorithms implemented in this software package are described in detail in the paper:**
A. Tsanas, G.D. Clifford: "Stage-independent, single lead EEG sleep spindle detection using the continuous wavelet transform and local weighted smoothing", Frontiers in Human Neuroscience 9:181, 2015

function [spindles_start_end, detected_spindles] = spindle_estimation_FHN2015(x, fs, spindle_frequency_range, alg_used)
%
% General call: spindles_start_end = spindle_estimation_FHN2015(x, fs);
%
%% Function for extracting sleep spindles from a single lead EEG data
%
% Inputs:  x            -> EEG data (vector)
%          fs           -> sampling frequency of the EEG
%__________________________________________________________________________
% optional inputs:
%          spindle_frequency_range  -> range over which to search for sleep
%                                      spindles                             [default: 11:16]
%          alg_used     -> Choose algorithm to apply to detect sleep spindles
%                          (currently supporting) 'a7' or 'a8'              [default: 'a7']
% =========================================================================
% Outputs: spindles_start_end -> sleep spindle onset (1st column), and spindle offset (2nd column), denoting sample into the time-series. The number of rows indicates the number of detected spindles in the data.
%          detected_spindles  -> Structure with additional information (primarily used for my debugging and additional information)
% =========================================================================
%
% Part of the "Thanasis_EEG_analysis" Toolbox
%
% -----------------------------------------------------------------------
% Useful references:
% 
% 1) A. Tsanas, G.D. Clifford: "Stage-independent, single lead EEG sleep 
% spindle detection using the continuous wavelet transform and local 
% weighted smoothing", Frontiers in Human Neuroscience 9:181, 2015
% -----------------------------------------------------------------------
%
% Last modified on 2nd August 2015
%
% Copyright (c) Athanasios Tsanas, 2015
%
% ********************************************************************
% If you use this program please cite:
%
% A. Tsanas, G.D. Clifford: "Stage-independent, single lead EEG sleep 
% spindle detection using the continuous wavelet transform and local 
% weighted smoothing", Frontiers in Human Neuroscience 9:181, 2015
% ********************************************************************
