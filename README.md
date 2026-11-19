# Pervious Concrete Mix Selector

A single-page, no-backend tool that compares four pervious concrete mixes on initial cost and 30-year maintenance cost, for a road of given length, width and traffic.

Built as a B.Tech project at IIT Tirupati by **Ayush Kumar (CE23B004)**.

## What it does

The user sets three inputs with sliders:

| Input | Range | Default |
|---|---|---|
| Road length | 0.5 to 5 km | 0.5 km |
| Road width | 3 to 4 m | 3.5 m |
| Initial commercial traffic | 1 to 97 CVPD | 30 CVPD |

For each mix (M1 to M4) the page shows:

- Slab thickness and concrete volume
- Initial cost under RMC supply and under on-site mixing
- Maintenance cost as a 30-year present value at 12%
- Total cost under each supply route

The mix with the lowest total cost is outlined in green. A maintenance breakdown and an ingredient take-off in kg are included below the main table.

## Design limits

The traffic slider is capped so the 20-year design MSA stays at or below 2.0. With 5% growth and a vehicle damage factor of 1.7, that cap is reached at 97 CVPD.

## Project structure

```
.
├── index.html   # Layout, embedded logo, and all calculation logic (vanilla JS)
├── style.css    # Dark theme styling
└── README.md
```

No build step, no dependencies, no external requests. Open `index.html` in a browser to run it.

## Running locally

```bash
git clone https://github.com/unfunnyayush/pavement-analysis-term-paper.git
cd pavement-analysis-term-paper
# open index.html in any browser
```

## Deploying on Vercel

1. Push the repository to GitHub.
2. In Vercel, choose **Add New → Project** and import the repository.
3. Leave the framework preset as **Other**. No build command or output directory is needed.
4. Deploy. The root `index.html` is served automatically.

## Where the numbers come from

All values are hardcoded from two workbooks in the project:

- **Initial cost workbook**: mix recipes, ingredient rates (on-site and RMC), labour and equipment schedule, slab thickness screening.
- **Life-cycle cost workbook**: sweeping, monitoring, pressure-wash events, corrective and rehabilitation schedule, end-of-life credit, discount rate.

The calculation reproduces the workbook totals exactly. For example, at 100 m × 3.5 m the M1 RMC material cost is ₹1,89,867.65, and at 3,500 m² the 30-year maintenance present value is ₹33,20,722.

## Limitations

These are the points to keep in mind before relying on the output.

- **Thicknesses are preliminary.** The 175 mm and 225 mm values come from a wheel-load screening and are not a final pervious concrete design. The screening does not link thickness to traffic.
- **Traffic does not change cost.** Traffic only sets the MSA value and the cap. The source workbooks have no traffic-to-cost link.
- **Mix ranking is fixed.** M1 is the lowest-cost mix at every input combination tested, because material is the only mix-specific cost and thickness is fixed per mix.
- **Maintenance is the same for all mixes.** It adds to each total but does not change the ranking.
- **Screening scope.** The source workbook's thickness screening is stated for up to 50 CVPD. The interface warns above that value.
- **Unverified assumptions.** The 0.8 flexural strength reduction and the 5% RMC discount are assumptions in the source workbook, not sourced figures.
- **Rates are proxies.** Rates are Andhra Pradesh SoR proxies or stated assumptions. Transport, subbase, GST and overhead are excluded. Verify against current quotations before use.

## Sources

- Mitrosz et al., *Materials* 2023, 16(15), 5222. [doi:10.3390/ma16155222](https://doi.org/10.3390/ma16155222). Source of the four mix recipes and reported strengths.
- IRC:37-2018, vehicle damage factor (indicative value only).
- IRC:SP:62-2014, wheel-load stress reference (conventional concrete, not validated for pervious concrete).
- Andhra Pradesh Standard Output Rates (SoR) 2026–27, labour, machinery and material rates.

## Author

**Ayush Kumar**
Roll number CE23B004
Department of Civil and Environmental Engineering, IIT Tirupati

## Licence

Academic project. Add a licence file if you intend to share or reuse the code.
