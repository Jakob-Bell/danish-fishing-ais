# 🚢 AIS Data Dictionary

This document provides the technical specifications for the AIS (Automatic Identification System) dataset. This data dictionary applies to point data from 2018 through 2025.

## 1. Core Identification & Temporal Data
These fields identify the vessel and the specific moment the data point was captured.

| # | Field Name | Description | Example | Type |
| :--- | :--- | :--- | :--- | :--- |
| 1 | **MMSI** | Maritime Mobile Service Identity: A unique 9-digit ID for the ship. | `477220100` | Text/Int32 |
| 2 | **BaseDateTime** | Full UTC date and time of the broadcast. | `2017-02-01T20:05:07` | DateTime |
| 9 | **IMO** | International Maritime Organization vessel number (Permanent ID). | `IMO9627980` | Text |
| 10 | **CallSign** | Call sign assigned to the vessel. | `VRME7` | Text |
| 8 | **VesselName** | Name as shown on the station radio license. | `OOCL Malaysia` | Text |

## 2. Positional & Movement Data
Real-time GPS and movement metrics. Note that some schemas use lowercase names (`latitude`, `longitude`).

| # | Field Name | Description | Units | Range / Domain |
| :--- | :--- | :--- | :--- | :--- |
| 3 | **LAT** | Latitude (decimal degrees). | Degrees | -89.99999 to 89.99999 |
| 4 | **LON** | Longitude (decimal degrees). | Degrees | -179.99999 to 179.99999  |
| 5 | **SOG** | Speed Over Ground: Vessel speed. | Knots | 0 to 99.9  |
| 6 | **COG** | Course Over Ground. | Degrees | 0 to 359.9 |
| 7 | **Heading** | True Heading: The direction the ship is pointing. | Degrees | 0 to 359  |

## 3. Vessel Characteristics & Status
Physical attributes and current operational state.

| # | Field Name | Description | Example | Units |
| :--- | :--- | :--- | :--- | :--- |
| 11 | **VesselType** | Type code (e.g., 70 = Cargo). | `70` | Integer |
| 12 | **Status** | Navigational status (e.g., 3 = Restricted maneuverability). | `3` | Integer |
| 13 | **Length** | Total length of the vessel. | `71.0` | Meters |
| 14 | **Width** | Total width of the vessel. | `12.0` | Meters |
| 15 | **Draft** | Depth of the vessel below the waterline. | `3.5` | Meters |
| 16 | **Cargo** | Cargo type code. | `70` | Integer |
| 17 | **Transceiver** | Class of AIS transceiver (A = Commercial, B = Leisure). | `A` | Text |

---

*Source: MarineCadastre.gov*
