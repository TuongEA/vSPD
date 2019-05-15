vSPD
====

vectorised Scheduling, Pricing and Dispatch


1. Remove revZoneEntry parameter because it is not used (vSPDSolve and vSPDModel)


2. Modify vSPDsolve.gms to faciliate CAN Refinements to National Market for Instantaneous Reserves (see below email)

From: David Bullen [mailto:David.Bullen@transpower.co.nz] 
Sent: Monday, 28 January 2019 2:06 p.m.
To: Tuong Nguyen
Cc: Phil Yao; Jeff Cowley
Subject: RE: CAN Refinements to National Market for Instantaneous Reserves

Hi Tuong


Thanks, happy new year. 

A summary of the SPD related changes for NMIR Refinements is as follows:

SPD inputs
In the RESERVESHARING section of the PERIOD file we have added an HVDCINITIAL column. This has been added for information purposes only, SPD does not use this value.

SPD outputs
There are no changes to the SPD outputs.

SPD changes
SPD pre-processing is changed so that the roundpower settings for FIR are now the same as for SIR. Specifically:
-              the RoundPowerZoneExit for FIR will be set at BipoleToMonopoleTransition by SPD pre-processing (same as for SIR), a change from the existing where the RoundPowerZoneExit for FIR is set at RoundPowerToMonopoleTransition by SPD pre-processing.
-              provided that roundpower  is not disabled by the MDB, the InNoReverseZone for FIR will be removed by SPD pre-processing (same as for SIR), a change from the existing where the InNoReverseZone for FIR is never removed by SPD pre-processing.

MDB logic
Changes have been made to the MDB view that sets the FIRROUNDPOWERDISABLED and SIRROUNDPOWERDISABLED values in the RESERVESHARING section of the PERIOD file (SPD pre-processing disables roundpower if the flag is set). The changes only apply to RTD and RTP schedules. Specifically: 
-              if cable discharge is active then the MDB view will disable roundpower for FIR, but not SIR, a change from the existing where cable discharge disables roundpower for SIR, but not FIR
-              if HVDC initial MW is > 190 then the MDB view will disable roundpower for SIR, a change from the existing where the check uses >= 190
-              if HVDC initial MW is > 190 then the MDB view will disable roundpower for FIR, a change from the existing where HVDC initial MW has no impact on FIR

SPD formulation
Because the formulation does  not specify how the roundpower boundaries are determined or how the ROUNDPOWERDISABLED flag is determined, and there are no changes to the SPD constraints themselves, there are no changes to the formulation.


Regards
David
