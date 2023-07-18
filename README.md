# Fishing Gear Classification from Vessel Trajectories and Velocity Profiles: Database and Benchmark

## ARTICLE

P. Melzi, J. M. Rodriguez-Albala, A. Morales, R. Tolosana, J. Fierrez, R. Vera-Rodriguez (2023). Fishing Gear Classification from Vessel Trajectories and Velocity Profiles: Database and Benchmark. In: A. Pertusa, A. J. Gallego, J. A. Sánchez, I. Domingues (eds) Pattern Recognition and Image Analysis. IbPRIA 2023. Lecture Notes in Computer Science, vol 14062. Springer, Cham. https://doi.org/10.1007/978-3-031-36616-1_50


## ABSTRACT

International Organizations demand to take care of our oceans and their ecosystems since they are of incalculable value to humanity. The illegal fishing activity does irreparable damage to these ecosystems and these organism are pushing to detect and combat illegal fishing activities. Fishing vessels are equipped with a radio frequency beacon that emits their GPS position and other information relevant to the Automatic Identification System (AIS). The GPS positions can be used to infer the vessel trajectories and detect illegal fishing activities. In this study we present a new database (https://github.com/BiDAlab/TrFGdb) including trajectories representing 5 different fishing gears, and analyze them as in a problem of time sequence analysis. We extract global and local features from the trajectories of vessels, and propose several supervised learning algorithms to classify the kinematics of vessels according to different fishing gears. Compared to previous works, we highlight the importance of considering trajectories with sampling period in the order of minutes instead of hours, to detect activities carried out in a short time that could help to distinguish fishing gears. A considerable effort has been dedicated to pre-processing the real data at our disposal, to generate a quality dataset with highly reliable labels. The best classification accuracy obtained in this study is 90%. We expect to improve it if more trajectories describing the different fishing gears were available.


## INSTRUCTIONS FOR DOWNLOADING TrFGdb 

1. [Download license agreement](https://github.com/BiDAlab/TrFGdb/blob/main/FishGear_License.docx), send by email one signed and scanned copy to atvs@uam.es and juanmanuel.rodrigueza@alumni.uam.es according to the instructions given in point 2.

2. Send an email to atvs@uam.es and juanmanuel.rodrigueza@alumni.uam.es, as follows:

    *Subject*: **[DATABASE benchmark: TrFGdb]**

    *Body*: Your name, e-mail, telephone number, organization, postal mail, purpose for which you will use the database, time and date at which you sent the email with the signed license agreement.

3. Once the email copy of the license agreement has been received at BiDA-Lab, you will receive an email with a username, a password, and a time slot to download the database.

4. [Download the benchmark](URL), for which you will need to provide the authentication information given in step 3. After you finish the download, please notify by email to atvs@uam.es that you have successfully completed the transaction.

5. For more information, please contact: atvs@uam.es and juanmanuel.rodrigueza@alumni.uam.es


## DESCRIPTION OF TrFGdb

|	Column	|	Type	|	Description	|
|	------	|	------	|	------	|
|	Id	|	int64	|	Row id	|
|	IdDiario	|	int64	|	Diary statement id	|
|	IdBuque	|	int64	|	Vessel id (AIS message)	|
|	FcSalida	|	date	|	Date/time of departure from port as declared in the Diary statement	|
|	FcRegreso	|	date	|	Date/time of return to port as declared in the Diary statement	|
|	IdPuertoSalida	|	int64	|	Departure port id declared in the Diary statement	|
|	IdPuertoRegreso	|	int64	|	Return port id declared in the Diary statement	|
|	ddaTiempoTrack	|	int64	|	Tracking time in minutes, calculated as the difference between FcRegreso and FcSalida	|
|	IdMensajeAISPuerto	|	int64	|	Row id of the result of the intersection of vessel's GPS positions (AIS message) with the geometric outline of the ports (MensajeAISPuerto ≈ map)	|
|	SpeedOverGround	|	float64	|	Speed in knots (AIS message)	|
|	Geom	|	object	|	Vessel's GPS position (AIS message). Spatial Reference ID (SRID): 4326 (WGS84)	|
|	X	|	float64	|	X coordinate of vessel's GPS position in degrees (longitude)	|
|	Y	|	float64	|	Y coordinate of vessel's GPS position in degrees (latitude)	|
|	CourseOverGround	|	float64	|	Course in degrees (AIS message)	|
|	FcMensaje	|	date	|	Date/time of transmission (AIS message)	|
|	Lapso	|	float64	|	Time between a GPS position and the previous one in seconds, calculated as the difference between FcMensaje(n) and FcMensaje(n-1)	|
|	Distancia	|	object	|	Distance between a GPS position and the previous one in nautical miles, calculated as the distance between Geom(n) and Geom(n-1)	|
|	DifSpeedOverGround	|	float64	|	Speed variation between a GPS position and the previous one in knots, calculated as the difference between SpeedOverGround(n) and SpeedOverGround(n-1)	|
|	AceleracionMedia	|	float64	|	Speed variation in a time interval between a GPS position and the previous one in knots/second, calculated as the difference between SpeedOverGround(n) and SpeedOverGround(n-1) per Lapso	|
|	DifCourseOverGround	|	float64	|	Course variation between a GPS position and the previous one in degrees, calculated as the difference between CourseOverGround(n) and CourseOverGround(n-1)	|
|	Track	|	int64	|	Track id	|
|	Item	|	int64	|	Ordinal id of a GPS position on the trajectory	|
|	mapIdPuertoSalida	|	int64	|	Departure port id obtained by intersection of vessel's GPS position with the geometric outline of a port	|
|	mapIdPuertoRegreso	|	int64	|	Return port id obtained by intersection of vessel's GPS position with the geometric outline of a port	|
|	mapFcSalida	|	date	|	Date/time of departure from port obtained as the date of transmission (FcMensaje) of a GPS position on departure from the geometric outline of a port	|
|	mapFcRegreso	|	date	|	Date/time of return to port obtained as the date of transmission (FcMensaje) of a GPS position when entering the geometric outline of a port	|
|	CuentaMensajes	|	int64	|	GPS position count (AIS messages) on a trajectory	|
|	Pesca	|	int64	|	0 on the subpath to/from the fishing area; 1 on the subpath where the fishing is performed, i.e. SpeedOverGround below 5 kn	|
|	mapTiempoTrack	|	int64	|	Track time in minutes, calculated as the difference between mapFcRegreso and mapFcSalida	|
|	MaxLapso	|	int64	|	Maximum time between a GPS position and the previous one in seconds, calculated as the maximum difference between FcMensaje(n) and FcMensaje(n-1)	|
|	CuentaMensajesPesca	|	int64	|	GPS position count (AIS messages) on the fishing subpath (Pesca = 1)	|
|	PorcentajeTiempoTrack	|	float64	|	Ratio between the track time according to the dates declared in the Diary statement and that obtained by intersection of the GPS positions and the geometric outlines of the ports, calculated as mapTiempoTrack/ddaTiempoTrack (or ddaTiempoTrack/mapTiempoTrack, whichever is less than 1)	|
|	PorcentajeMensajesPesca	|	float64	|	Ratio of the GPS position count (AIS messages) on the fishing subpath to the GPS position count (AIS messages) on the track, calculated as CuentaMensajesPesca/CuentaMensajes	|
|	ArteDiario	|	object	|	Grouping of fishing gears declared in the Diary statement (target)	|


## REFERENCES

1. Chuaysi, B., Kiattisin, S.: Fishing vessels behavior identification for combating IUU fishing: enable traceability at sea. Wirel. Pers. Commun. 115(4), 2971–2993 (2020) [[CrossRef](https://doi.org/10.1007%2Fs11277-020-07200-w)] [[Google Scholar](https://scholar.google.com/scholar_lookup?&title=Fishing%20vessels%20behavior%20identification%20for%20combating%20IUU%20fishing%3A%20enable%20traceability%20at%20sea&journal=Wirel.%20Pers.%20Commun.&volume=115&issue=4&pages=2971-2993&publication_year=2020&author=Chuaysi%2CB&author=Kiattisin%2CS)]

2. Dunn, D.C., et al.: Empowering high seas governance with satellite vessel tracking data. Fish Fish. 19(4), 729–739 (2018) [[CrossRef](https://doi.org/10.1111%2Ffaf.12285)] [[Google Scholar](https://scholar.google.com/scholar_lookup?&title=Empowering%20high%20seas%20governance%20with%20satellite%20vessel%20tracking%20data&journal=Fish%20Fish.&volume=19&issue=4&pages=729-739&publication_year=2018&author=Dunn%2CDC)]

3. European Union: Regulation (EU) no 1379/2013 of the European parliament and of the council of 11 December 2013 on the common organisation of the markets in fishery and aquaculture products, amending council regulations (EC) no 1184/2006 and (EC) no 1224/2009 and repealing council regulation (EC) no 104/2000 (2013). https://eur-lex.europa.eu/legal-content/EN/TXT/?uri=celex%3A32013R1379. Accessed 21 Nov 2022

4. Fierrez, J., Ortega-Garcia, J., Ramos, D., Gonzalez-Rodriguez, J.: Hmm-based on-line signature verification: feature extraction and signature modeling. Pattern Recogn. Lett. 28(16), 2325–2334 (2007) [[CrossRef](https://doi.org/10.1016%2Fj.patrec.2007.07.012)] [[Google Scholar](https://scholar.google.com/scholar_lookup?&title=Hmm-based%20on-line%20signature%20verification%3A%20feature%20extraction%20and%20signature%20modeling&journal=Pattern%20Recogn.%20Lett.&volume=28&issue=16&pages=2325-2334&publication_year=2007&author=Fierrez%2CJ&author=Ortega-Garcia%2CJ&author=Ramos%2CD&author=Gonzalez-Rodriguez%2CJ)]

5. Food and Agriculture Organization of the United Nations: What is IUU fishing? (2022). https://www.fao.org/iuu-fishing/background/what-is-iuu-fishing/en/. Accessed 17 Nov 2022

6. Jarvis, R.M., Young, T.: Pressing questions for science, policy, and governance in the high seas. Environ. Sci. Policy 139, 177–184 (2023) [[CrossRef](https://doi.org/10.1016%2Fj.envsci.2022.11.001)] [[Google Scholar](https://scholar.google.com/scholar_lookup?&title=Pressing%20questions%20for%20science%2C%20policy%2C%20and%20governance%20in%20the%20high%20seas&journal=Environ.%20Sci.%20Policy&volume=139&pages=177-184&publication_year=2023&author=Jarvis%2CRM&author=Young%2CT)]

7. Leonard, K.: Schaum’s Outline of Business Statistics, 4th edn. (2003) [[Google Scholar](https://scholar.google.com/scholar?&q=Leonard%2C%20K.%3A%20Schaum%E2%80%99s%20Outline%20of%20Business%20Statistics%2C%204th%20edn.%20%282003%29)]

8. Martinez-Diaz, M., Fierrez, J., Krish, R.P., Galbally, J.: Mobile signature verification: feature robustness and performance comparison. IET Biometrics 3(4), 267–277 (2014) [[CrossRef](https://doi.org/10.1049%2Fiet-bmt.2013.0081)] [[Google Scholar](https://scholar.google.com/scholar_lookup?&title=Mobile%20signature%20verification%3A%20feature%20robustness%20and%20performance%20comparison&journal=IET%20Biometrics&volume=3&issue=4&pages=267-277&publication_year=2014&author=Martinez-Diaz%2CM&author=Fierrez%2CJ&author=Krish%2CRP&author=Galbally%2CJ)]

9. Marzuki, M.I., Gaspar, P., Garello, R., Kerbaol, V., Fablet, R.: Fishing gear identification from vessel-monitoring-system-based fishing vessel trajectories. IEEE J. Oceanic Eng. 43(3), 689–699 (2017) [[CrossRef](https://doi.org/10.1109%2FJOE.2017.2723278)] [[Google Scholar](https://scholar.google.com/scholar_lookup?&title=Fishing%20gear%20identification%20from%20vessel-monitoring-system-based%20fishing%20vessel%20trajectories&journal=IEEE%20J.%20Oceanic%20Eng.&volume=43&issue=3&pages=689-699&publication_year=2017&author=Marzuki%2CMI&author=Gaspar%2CP&author=Garello%2CR&author=Kerbaol%2CV&author=Fablet%2CR)]

10. Miller, R.J., et al.: Big data curation. In: COMAD, p. 4 (2014) [[Google Scholar](https://scholar.google.com/scholar?&q=Miller%2C%20R.J.%2C%20et%20al.%3A%20Big%20data%20curation.%20In%3A%20COMAD%2C%20p.%204%20%282014%29)]

## ACKNOWLEDGMENTS

We thank Tragsatec’s Management of Agricultural and Fisheries Information Systems and the General Secretariat of Fisheries of the Spanish Ministry of Agriculture, Fisheries and Food for the data and expertise provided to carry out the study. This project has received funding from the European Union’s Horizon 2020 research and innovation programme under the Marie Skłodowska-Curie grant agreement No 860813 - TReSPAsS-ETN. This study is also supported by the project INTER-ACTION (PID2021- 126521OB-I00 MICINN/FEDER).
