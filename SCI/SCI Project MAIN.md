## Questions

| area                     | questions                                                                                                              | ideas                                                                                                              |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
| travel agencies          | How the biggest Online Travel Agencies are investing in Generative AI? Can smaller Travel Agencies still be relevant?  | read financial reports of OTA, look for startups, statista                                                         |
| accommodation businesses | What is the impact of GenAI on accommodation businesses? Will OTAs choices impact them considerably?                   | opendormire and booking, ota's fees                                                                                |
| countries                | Are other countries in the EU investing in GenAI? How and how much?                                                    | statista, countries reports                                                                                        |
| public                   | Can Destination Management Organizations (DMO) use Generative AI to improve efficacy in attracting tourists?           | genAI for marketing, enit reports                                                                                  |
| tourist                  | Phases of customer journey in travel planning where GenAI is relevant? Will the planning and booking behaviour change? | article, different customer journey based on customer/travel type (ie luxury), twitter to know how chatgpt is used |
| rights                   | Are accommodation businesses and consumers rights threatened? Are there new policies required?                         |                                                                                                                    |


## 1. About OTA
| area            | questions                                                                                                             |
| --------------- | --------------------------------------------------------------------------------------------------------------------- |
| travel agencies | How the biggest Online Travel Agencies are investing in Generative AI? Can smaller Travel Agencies still be relevant? |

*sources*
- Statista - AI on tourism [here](https://www.statista.com/topics/10887/artificial-intelligence-ai-use-in-travel-and-tourism/#topicOverview) and [here](https://www.statista.com/topics/2704/online-travel-market/#topicOverview) and [here](https://www.statista.com/outlook/mmo/travel-tourism/italy?currency=EUR#revenue)
- [OliverWyman-GENERATIVE AI’S INFLUENCE ON LEISURE TRAVELER BEHAVIORS](https://www.oliverwyman.com/our-expertise/insights/2023/oct/generative-ai-leisure-traveler-trends.html)
- AIDA?

*dataset*
List all the biggest Travel Agencies in italy.
Variables
- name
- online/traditional
- revenue
- country
- investment in ai

Ho scaricato da AIDA le aziende con codice ateco 7911 (Attività delle agenzie di viaggio). Contenuti del database Aida - Informazioni anagrafiche e finanziarie dettagliate su circa 980.000 imprese aggiornate all’ultimo anno disponibile; - Serie Storica di bilanci contenuti fino a 10 anni;
![[Pasted image 20240507185445.png]]

Su Statista ci sono le più grandi OTA. Ci vorrebbe un menù a tendina per selezionare uno dei due dataset oppure quello completo per confronto.


*Show*

| topic | PLOT                                                   | source                  |
| ----- | ------------------------------------------------------ | ----------------------- |
|       | 10 biggest otas                                        | statista                |
|       | ota investments in ai (how many projects and how much) | financial report of ota |
|       | where are ota located?                                 |                         |
|       | how many travel agencies in italy                      |                         |
|       | compare revenue of ota vs tta in italy                 |                         |



## 2. About accommodation businesses

| accommodation businesses | What is the impact of GenAI on accommodation businesses? Will OTAs choices impact them considerably?                   | opendormire and booking, ota's fees                                                                                |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |
*ideas*
- statista
- count how many italian accomodation businesses are present in the top 3 OTA (booking, expedia, airbnb)
	- compare number of acc.bss. on operdormire with the number on ota
- understand OTA's fees
- AIDA
- airbnb data [here](https://insideairbnb.com/get-the-data)

*dataset*
List all the accommodation businesses in italy.
Variables
- name
- provincia
- regione
- website y/n
- fees on booking
- fees on expedia
- fees on airbnb

(add a button to increase in percentage the fees based on statista estimations)

Ho scaricato da AIDA la lista con codice ateco 55 - ALBERGHI E STRUTTURE SIMILI
soltanto aziende attive.

Forse le aziende non sono una buona idea.
Meglio provare con le strutture ricettive delle grandi città (Roma, Milano, Bologna).
E verificare se sono su airbnb, booking e ? stimando quanto pagano di fees in media.

| topic | PLOT                                                                                                   | source                |
| ----- | ------------------------------------------------------------------------------------------------------ | --------------------- |
|       | how many acc.bus. have a website?                                                                      |                       |
|       | count how many italian accomodation businesses are present in the top 3 OTA (booking, expedia, airbnb) | compare dataset with? |
|       | how much are the fees in ota?                                                                          |                       |



## 3. About countries

| countries                | Are other countries in the EU investing in GenAI? How and how much?                                                    | statista, countries reports                                                                                        |
| ------------------------ | ---------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------ |

*sources*
1. https://aiindex.stanford.edu/report/
	1. https://drive.google.com/drive/folders/15JTCpcQ8R_Vl36qEjcitiYDssYnSg4oF
		1. 4.3.6
		2. 4.3.17 for new ai companies worldwide (source?)
2. https://ourworldindata.org/artificial-intelligence
3. https://cat.eto.tech/?expanded=Summary-metrics

4. [eu genAI investments](https://www.europarl.europa.eu/RegData/etudes/ATAG/2024/760392/EPRS_ATA(2024)760392_EN.pdf)
5. https://epthinktank.eu/2024/04/04/ai-investment-eu-and-global-indicators/#:~:text=The%20EU%20and%20the%20United,billion%20in%20US%20AI%20companies.
6. https://www.euronews.com/business/2024/04/29/who-in-europe-is-investing-the-most-in-artificial-intelligence
7. https://ai-watch.ec.europa.eu/index_en

*dataset*
List of all countries in the world. (use default with gdp > t or gdp/pop > t).
Variables
- name
- continent
- population
- gdp
- pernottamenti [here](https://www.enit.it/storage/202402/20240219122646_il%20posizionamento%20dellitalia%20i%20trend%20in%20atto%20-%20maria%20elena%20rossi%20-%205%20febbraio%202024%20-%20bit%202024.pdf)
- strategy for ai ([here](https://ourworldindata.org/artificial-intelligence))
- investment in AI by year?

(Maybe add a list of italian startups of genAI?)


*show*

| topic | PLOT                               | source          |
| ----- | ---------------------------------- | --------------- |
|       | major investments in ai by country | aiindex         |
|       | in eu?                             |                 |
|       | startup italiane di gen AI         | dataset startup |

## Bonus Dataset
Startup innovative in italia.



## Additional Notes

*Ideas*
1. read financial reports of OTA
2. look for startups about genAI and Hospitality
3. statista
4. dataset di startup italiane?

*Data*
- [istat viaggi](https://www.istat.it/it/archivio/295812)
- Eurostat
- Statista - AI on tourism [here](https://www.statista.com/topics/10887/artificial-intelligence-ai-use-in-travel-and-tourism/#topicOverview)
	- and related like [this](https://www.statista.com/topics/7589/digitalization-of-the-travel-industry/#topicOverview)
	- and [this](https://www.statista.com/statistics/934995/revenue-of-leading-otas-worldwide/) about best otas
- [OliverWyman-GENERATIVE AI’S INFLUENCE ON LEISURE TRAVELER BEHAVIORS](https://www.oliverwyman.com/our-expertise/insights/2023/oct/generative-ai-leisure-traveler-trends.html)
	- with interesting survey
- [database strutture toscana ](https://dati.toscana.it/dataset/movimento-dei-clienti-e-struttura-dell-offerta-ricettiva-toscana-anno-2023)
- [enit](https://www.enit.it/it/research-library)
- [airbnb statista](https://www.statista.com/statistics/1084927/number-of-airbnb-listings-in-selected-italian-cities/)

*Articles*

- [investimenti ai in italia](https://www.ansa.it/canale_tecnologia/notizie/future_tech/2024/03/25/ia-nel-2024-in-italia-investimenti-in-crescita-del-68_a82e2b94-01af-423d-ab91-650fb14c1ede.html)
- [travel OTA genAI](https://econsultancy.com/travel-ota-generative-ai/)
- [eu approach to ai](https://digital-strategy.ec.europa.eu/en/policies/european-approach-artificial-intelligence)
- [accenture](https://www.accenture.com/us-en/insights/travel/travel-ai-maturity)
- [time](https://time.com/6290940/ai-travel-industry/)
- [OliverWyman](https://www.oliverwyman.com/our-expertise/insights/2023/oct/generative-ai-leisure-traveler-trends.html)
- [PNRR e hub del turismo](https://www.italiadomani.gov.it/content/sogei-ng/it/it/Interventi/investimenti/hub-del-turismo-digitale.html)
- [booking.com on AI](https://business.booking.com/resource-hub/articles/business-travel-and-ai/?aid=2139500%3Blabel%3DORG_Z29vZ2xlX19PUyBYX0Nocm9tZV8xNzE1MTc2MjY0X3Jlc291cmNlLWh1Yi9hcnRpY2xlcy9idXNpbmVzcy10cmF2ZWwtYW5kLWFpX0J1c2luZXNzIHRyYXZlbCByZXNvdXJjZXMgfCBCb29raW5nLmNvbSBmb3IgQnVzaW5lc3NfaXQtaXRfSVQ%3D)



*Papers*
- Paper on CrunchBase startups in Tourism and AI [here](https://www.emerald.com/insight/content/doi/10.1108/IJCHM-02-2021-0220/full/html) (PDF)


`TITLE-ABS-KEY ( travel AND hospitality AND tourism AND ( chatgpt OR ( generative AND ai ) OR llm OR "Large Language Model" ) )`

maybe better
`TITLE-ABS-KEY ( travel AND tourism AND ( chatgpt OR ( generative AND ai ) OR llm OR "Large Language Model" ) )`

*Companies*
- [nearform travel agent](https://www.nearform.com/digital-community/augmenting-user-experiences-using-llms-an-analysis-of-our-travel-ai-agent-application/)
- [tourism innovation companies in italy](https://www.ministeroturismo.gov.it/wp-content/uploads/2023/06/DVPT_STP_Decreto-di-approvazione-graduatoria-startup_signed_1206823.pdf)
- https://www.leewayhertz.com/chatgpt-for-tourism/


*Marketing-related*
- [ENIT per dmo](https://www.enit.it/it/dmo-italiane)
- [Co-creating with ChatGPT for tourism marketing materials](https://www.sciencedirect.com/science/article/pii/S2666957924000065)

*might be useful in the future*
- https://ieeexplore.ieee.org/document/10468915
- https://www.tandfonline.com/doi/full/10.1080/13683500.2023.2300032?scroll=top&needAccess=true

## Other datasets

![[Dataset]]