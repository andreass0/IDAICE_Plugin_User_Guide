(Introduction)=

# Introduction

## What is the RFEM-Plugin?

The RFEM-plugin (in the following referred to as "the plugin") enables structural analysis with the finite element
software [RFEM 6 by Dlubal](https://www.dlubal.com/en/downloads-and-information/documents/online-manuals/rfem-6) for the
SIMULTAN-data model. This is achieved by exporting all necessary data for rudimental structural analysis into an
XML-file which can be imported into RFEM 6.

## Functionality covered by the RFEM-Plugin

In the current state of development the plugin is able to export:

- Geometry
- Material data
- Loads
    - Nodal
    - Line
    - Surface
- Supports with certain nonlinear behaviour
    - Nodal
    - Line
    - Surface
- Structural components and their hinges with certain nonlinear behaviour
    - Beams
    - Columns
    - Surfaces

What we are not able to do right now:

- Import results back into the SIMULTAN-data model (since in its current state there is now mesh visualization
  implemented in SIMULTAN-data model)
- Track changes made in the RFEM-data model but not in the SIMULTAN-data model

## Project

The development of the RFEM-Plugin is the result of the FFG-research project "Ganzheitliche Gebaeudesimulation"
supervised by Christoph Bauer. Additional information about the project and project outcomes can be found under these
links:

- [Ganzheitliche Gebaeudesimulation Press](https://www.woschitzgroup.com/news/bim-war-gestern/)
- [RFEM Plugin Publication](XXXX)
- [IDA-ICE Plugin Publication](XXX)
- [Additional works](XXXX)

Information and publications about SIMULTAN:

- [SIMULTAN as a Big-Open-Real-BIM Data Model - Proof of Concept for the Design Phase](https://repositum.tuwien.at/handle/20.500.12708/62532)
  {cite}`paskalevaSIMULTANBigOpenRealBIMData2019`
- [Digital Twin applications using the SIMULTAN data model and Python](#) {cite}`buhlerDigitalTwinApplications2022`
- SIMULTAN as a Big-Open-Real-BIM Data Model - Proof of Concept for the Design Phase
  {cite}`paskalevaSIMULTANBigOpenRealBIMData2019`
- SIMULTAN - Simultane Planungsumgebung fuer Gebaeudecluster in resilienten, ressourcen- und hoechst energieeffizienten
  Stadtteilen {cite}`bednarSIMULTANSimultanePlanungsumgebung`

## Authors

Project supervision of the development of the RFEM-Plugin was done by Andreas Sarkany and Bernhard Steiner. Core
development of the software was conducted by Zsombor Jarosi. Additional Feedback and testing was provided by Thomas Rabl
and Thomas Bednar.

## Getting help

You can get in touch with the authors via the Issue-Tracker of the repository this user guide is published on.