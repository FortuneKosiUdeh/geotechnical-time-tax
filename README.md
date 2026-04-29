# The Geotechnical Time Tax
### A Pilot Study Linking Subsidence, Transit Delay, and Neighborhood Equity in Boston

---

Large portions of Boston were constructed by filling tidal marshes and mudflats throughout the 19th century. Unlike bedrock, unconsolidated fill continues to compress under its own weight for decades — a process called differential settlement. This study asks whether that ongoing geological process leaves a measurable signature in the MBTA's own safety record, and whether the communities most exposed to it are also the least economically resourced to absorb the cost.

The central claim is a four-link causal chain: filled land subsides unevenly, uneven subsidence bends track geometry, bent geometry triggers MBTA speed restrictions (slow zones), and slow zones impose commute delays that fall disproportionately on lower-income riders.

The analysis integrates four data streams. MBTA GTFS data provides the geographic geometry of the Red, Orange, Blue, and Green Line corridors along with the locations of documented slow zones. A digitized 1840s shoreline boundary — derived from historical survey records — defines the spatial extent of filled land. Sentinel-1 InSAR satellite measurements provide a grid of vertical land motion (VLM) rates, expressed in millimeters per year, for the Boston metropolitan area. American Community Survey data supplies median household income at the census-tract level for Suffolk County.

The structural stress at each track segment is quantified using the beam-bending relationship

$$S = E \cdot \frac{d^2w}{dx^2}$$

where $E$ is the elastic modulus of the rail system (approximately 200 GPa for Grade 900A steel), $w(x)$ is the vertical displacement field derived from InSAR measurements, and $d^2w/dx^2$ is the curvature of the settlement profile — the second spatial derivative of subsidence. It is this curvature, not uniform sinking, that degrades track geometry and mandates speed restrictions. This quantity is termed the Subsidence Impact Factor (SIF).

Preliminary results indicate that 57% of documented slow zones fall within the 1840s landfill footprint, against an expected rate of approximately 22% given the footprint's share of the network — a 3.2-fold spatial enrichment. Track segments on filled land show mean VLM rates of approximately −4.2 mm/yr, compared to −1.1 mm/yr on stable bedrock. Neighborhoods adjacent to landfill slow zones have a median household income roughly $28,000 lower than stable-corridor neighborhoods, and their commuters accumulate an estimated 4.3 times more annual delay. The Pearson correlation between neighborhood median income and annual delay burden is approximately −0.87.

The InSAR measurements and per-segment delay values in the current analysis are calibrated synthetic placeholders, pending ingestion of live Sentinel-1 products and official MBTA LAMP travel-time records. The spatial overlap finding is based on real data. The analytical framework is otherwise complete and production-ready.

---

**Author:** Fortune Kosi Udeh — Boston, MA
