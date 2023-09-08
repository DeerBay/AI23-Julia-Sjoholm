# Workflow for AI-projects

## Insamling av data, format, lagring
Statistikdata skulle kunna hämtas från exempelvis Svensk Mäklarstatistik som tillhandahåller detaljerad objektsdata och statistik över försäljningar från hela Sverige. Den innehåller uppgifter så som slutpriser, uppgifter om hur många boendeenheten var som såldes, uppgifter om fastighetens totala storlek vid försäljningar av villor eller andra fastigheter (markytan) men även uppgifter som hur nära vatten fastigheten ligger och många fler attribut. Ett annat alternativ skulle vara att välja att tanka hem data från kaggel.com som tillhandahåller en stor mängd öppna data som kan användas till att bygga maskininlärnings modeller. 

Det finns flera alternativ för vilka format vi kan välja att bevara våra data i. Viktigt att ha i åtanke är att projektets data ska vara möjlig att återanvända för en lång tid framöver. På Svensk Nationell datatjänsts hemsida kan vi läsa att den bör vara vanligt förekommande, kunna läsas av flera program samt, vara öppna  samt icke-proprietär. Deras rekommendationer för statiska data är formaten .CSV, SIARD och SQL.

Man kan ladda data på en lokal server om utrymme och möjligheter för det existerar, en annan möjlighet är att förvara det i någon molntjänst.

## Visualisering av data
Visualisering, eller grafiska presentation, kan göras med hjälp av diagram eller kartor. Grafen skulle då kunna visa hur antal kvadrat på en lägenhet hade en korrelation med slutpriset eller att närheten till vatten påverkade slutpriset. Ett hjälpmedel som vi skulle kunna använda är då matplotlib (se nedan bild)

Bearbeta data till rätt format
En start för att processa och börja preparera den data som ska ingå i modellen är att bestämma vilka värden/attribut vi ska använda oss av. Är det bara kvadratmeter och boytan, eller ska man ha flera värden så som antal rum, skick på fastigheten, uppgifter om det finns en pool ock så vidare. 

När vi väl har avgränsat vilka värden som är av signifikans för våra slutpriser börjar vi tvätta bort de oönskade värdena i vårt dataset samt tar bort extremer för de värden som valts att användas. Det gäller då värden som sticker ut avsevärt från mängden då dessa kan påverka vår slutgiltiga modell åt något håll. Vi behöver också se till att det är representativ data vi använder oss av. Om vi bara skulle träna modellen på data innehållande slutpriser på hus på Lidingö i Stockholm eller bara från Haparanda  osv. Skulle vi vilja göra en modell för enbart de områdena hade det kunnat fungera men om vi önskar en mer generell modell för huspriser i Sverige måste den representera hela landet. Vi behöver också behandla saknade värden, antingen genom att raderna tas bort, ges ett snittvärde alternativt interpolerande värden (värden som ligger i närheten av andra värden).

![Visualisering av data](exercises\pictures\numpy.jpg)

## Linjär regression
Linjär regression används ofta i samband med en regressionsanalys. Det är den mest grundläggande typen av regressionsmodell. Det innebär ett linjärt förhållande mellan variablerna i datan. Om den ena variabeln ökar eller minskar kommer också den andra variabeln öka eller minska.

Den innehåller en beroende och en oberoende variabel. Den beroende variabelns värde antas bero av en eller flera andra variabler. Det finns också oberoende variable vars värde inte ändras beroende på några andra variablers värde som man använder sig av i analysen. 

I vårt exempel med fastigheter skulle man kunna säga att avståndet till vatten är en oberoende variabel medans priset på fastigheten är en beroende variabel. Om avståndet till vatten minskar kan vi anta att priset kommer att påverkas, däremot om priset ökar är det inte givet att avståndet till vattnet minskar.

## Hur kan man göra för att driftsätta modellen?

När själv modellen är redo och man känner sig nöjd med resultatet av träningen och testningen är det dags för att driftsätta modellen så att användarna kan ta del av den. Vid driftsättningen eller implementeringen är det viktigt att ha en driftsättningsmiljö med rätt hårdvara och data. Du behöver containers, notebooks och in-app environments. Containers omfattar all hårdvara, konfigurationer och beroenden som krävs för att distribuera modellen. Anteckningeböcker kan till exempel vara Jupyter. In-App environments används när det finns vissa begränsningar kring användning av data utanför applikationen.

Gällande vår data skulle det fungera bra att göra en app där användaren kunde välja att göra sökningar som vad huspriserna ligger på snitt i ett visst område, alternativt stoppa in värden som storlek på hus, storlek på fastighet, närhet till vatten o.s.v. för att sedan få ut ett estimerat värde vad det kunde sälja huset/lägenheten för idag.

## Teknologier kan man använda i de olika stegen i maskininlärningsprocessen

Vi har ovan gått igenom två av stegen i maskininlärning, dels datainsamling och en del av pre-processing av data. 

Vid pre-processing av data kan man använda sig av Python, NumPy och Pandas. Man kan ladda upp .CSV i Pandas. Pandas är ett programvarubibliotek för datamanipulering och analys. När du väl ordnat datan konverterar du din data frame med hjälp av NumPy till flerdimensionella listor. Datan delas sedan in i ett tränings-set och ett test-set. 

I vårt fall är modellen redan vald, supervised learning med algoritmen linjär regression, för vår maskininlärningsmodell. Men viktigt att tänka på är att göra sin research ordentligt innan för att se att den modellen du väljer verkligen passar just ditt projekt.

När du tränar modellen, betyder det att du bygger modellen egentligen med hjälp av träningsdatan. Du testar sedan modellen mot testdatan för att se att den ger samma resultat. När dessa stämmer överens och modellen känns applicerbar kan vi börja förutse nya värden.

I utvärderingen är det viktigt att ställa frågor som är det en användbar modell, skulle den bli bättre med mer data eller andra features till exempel.

1.	Gathering data
2.	Data pre-processing
3.	Researching the model that will be best for the type of data
4.	Training and testing the model
5.	Evaluation

![ML Model deployment](pictures\Machine_Learning_Model_Deployment_Tutorial.webp)

### *Källor:*
Svensk Nationell datatjänst 
(https://snd.gu.se/sv/hantera-data/guider/att-valja-filformat) 2023-09-04

Kaggel (https://www.kaggle.com/)

Pluralsight – Preparing Data for Machine Learning by Janani Ravi
https://app.pluralsight.com/library/courses/preparing-data-machine-learning/
 
”Vad är linjär regressionsanalys”
https://www.hypergene.se/sv/kunskapsbank/blogg/vad-ar-en-regressionsanalys-och-hur-gor-man/

Linear regression
https://www.w3schools.com/python/python_ml_linear_regression.asp
https://www.tutorialspoint.com/linear-regression-using-python

Plotting Linear Regression
https://www.tutorialspoint.com/linear-regression-with-matplotlib-numpy


Steg i maskininlärning
https://www.kdnuggets.com/2018/12/machine-learning-project-checklist.html

Workflow of a Machine Learning project
https://towardsdatascience.com/workflow-of-a-machine-learning-project-ec1dba419b94

Deployments methods
https://streamsets.com/blog/four-machine-learning-deployment-methods/
Machine Learning Model Deployment- A Beginner’s Guide (projectpro.io)
