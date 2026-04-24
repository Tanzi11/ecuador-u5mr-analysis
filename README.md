# ecuador-u5mr-analysis

Evaluating the impact of World Bank development interventions on 
under-5 mortality rates (U5MR) in Ecuador using synthetic control 
methodology.

## Research Question

Did World Bank interventions beginning in 1992 accelerate the 
reduction of under-5 mortality in Ecuador beyond what would have 
been expected given regional trends?

## Methodology

This analysis applies the synthetic control method (Abadie & 
Gardeazabal, 2003) to construct a weighted counterfactual 
"Synthetic Ecuador" from a donor pool of comparable Latin American 
economies. The difference between actual and synthetic Ecuador 
post-1992 is interpreted as the estimated treatment effect.

**Donor pool:** Bolivia, Colombia, Dominican Republic, Mexico, 
Paraguay, Peru

Countries excluded from the donor pool: Brazil and Chile (scale 
incompatibility), Costa Rica and Uruguay (atypical child health 
trajectories for the region).

**Predictors:** Fertility rate, GDP per capita (constant 2015 USD), 
immunization DPT coverage, with special predictors at 1982, 1985, 
and 1991 mean U5MR values.

**Treatment year:** 1992

## Data

All data sourced directly from the World Bank Development Indicators 
API via `wbgapi`. No local files required — the notebook is fully 
reproducible from the API pull.

| Indicator | Code |
|-----------|------|
| Mortality rate, under-5 | SH.DYN.MORT |
| Fertility rate, total | SP.DYN.TFRT.IN |
| Immunization, DPT | SH.IMM.IDPT |
| GDP per capita (constant 2015 USD) | NY.GDP.PCAP.KD |

## Results

Donor weights assigned by the optimizer:

| Country | Weight |
|---------|--------|
| Colombia | 0.250 |
| Paraguay | 0.204 |
| Dominican Republic | 0.202 |
| Mexico | 0.144 |
| Peru | 0.117 |
| Bolivia | 0.083 |

The path plot shows Ecuador's U5MR declining faster than the 
synthetic counterfactual from 1992 onwards, with a sustained gap 
of approximately 5-6 deaths per 1,000 live births by 2000.

However, the placebo test indicates this gap is not statistically 
distinguishable from donor country placebos. The observed decline 
likely reflects broader regional trends in child mortality reduction 
rather than a treatment effect attributable specifically to World 
Bank interventions. This null finding is itself informative — it 
suggests that Ecuador's improvement was consistent with regional 
momentum rather than anomalous, raising questions about intervention 
attribution in contexts of widespread regional progress.

## Limitations

- Pre-treatment fit shows a slight negative gap beginning in the 
  late 1980s, suggesting Ecuador may have already been on a 
  favorable trajectory prior to 1992
- GDP per capita PPP constant 2021 was replaced with constant 2015 
  USD due to insufficient historical coverage for 1980s Latin America
- Treatment year reflects a period of significant WB health sector 
  engagement in Ecuador; specific program identification was outside 
  the scope of this analysis

## Requirements

pip install pysyncon wbgapi pandas matplotlib

## Usage

All analysis is contained in `analysis.ipynb`. Run cells 
sequentially. No local data files required.

## Collaborators

Analysis conducted in collaboration with Stephen Porter.
