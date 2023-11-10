# Hackaday Supercon 2023 Vectorscope 
### KiCad Redrawing Project

This is a port of the Vectorscope schematics into KiCad. 
It is also a partially-complete KiCad project using Voja Antonic's original 
Circuit Maker PCB design as converted into KiCad PCB format by Thomas Flummer.

## Status

* Schematics created, first pass error checking complete. It has not been
meticulously compared with the original schematics.

* Symbols have been collected into a single project library:
  `vector.kicad_sym`

* New footprints, as needed, will go into a single project library:
  `vector.pretty`

* Original footprints extracted from the PCB and stored into a single
  project library: `vector-orig.pretty`

* So far, the changes to the original converted PCB are minimal and
  coule be easily replicated should the Circuit Maker design be updated:
  - footprints changed to point to `vector-orig.pretty`
  - graphical lines converted to KiCad PCB traces

## Issues

#### PCB Changes, traces

As noted above, the circuit traces on the PCB, as converted, are just
graphical lines. These can easily be changed into PCB traces using the
built-in `Create Tracks from Selection` option (Kicad v7).

#### PCB Changes, footprints (TBD)

Some parts in the PCB don't have the expected footprints, but are instead just
a collection of features. For example, the three each 0.1 inch IO pin-header 
connectors appear instead as 20 separate "footprints", each one a single
pad. I have investigated how to fix these, and it is pretty straightfoward:

* IO connectors, 
  - Scope Input, 1x4
  - Signal Generator Output, 1x4
  - IO Connector, 1x12
* Speaker
* Two SMT test pads (external power?)
* Slide switch
* Battery holders

#### Schematics

The following errors have been identified in the original schematics:

* Capacitor C16 seems to be duplicated (not 100% confirmed)
* TPA321 Speaker amplifier connects to +3V3, not +3V3F
* Some not-connected Pico pins are not shown on the original

#### Part Footprint Mismatches

Several discrete parts in the original PCB file are not consistent
between three different sources: the footprint itself, the assocaited 3D
file, and the real part as idenified in the BOM. These are as follows:

* LEDs
  - footprint: 0603
  - 3D file: 0603 
  - BOM: 0805 

* Resistors
  - footprint: Tantalum Kemet C (note 1)
  - 3D file: 0603
  - BOM 0805

* Capacitors, 2.2uF and 100nF
  - footprint: Tantalum Kemet C (note 1)
  - 3D file: 0603
  - BOM 0603

* Capacitors, 22uF
  - footprint: Voja custom part
  - 3D file: EIA 3528/Kemet T (note 2)
  - BOM: 1210


Note 1: The Tantalum Kemet C package is EIA 6023, which about the size 
of an EIA 2512 resistor. 

Note 2: Tantalum Kemet T packate is EIA 3528, which is a bit largeer than
an EIA 1210 resistor.


![](vectorscope-sch.png)
