{\rtf1\ansi\ansicpg1252\cocoartf1404\cocoasubrtf470
{\fonttbl\f0\fswiss\fcharset0 Helvetica;}
{\colortbl;\red255\green255\blue255;}
\paperw11900\paperh16840\margl1440\margr1440\vieww10800\viewh8400\viewkind0
\pard\tx566\tx1133\tx1700\tx2267\tx2834\tx3401\tx3968\tx4535\tx5102\tx5669\tx6236\tx6803\pardirnatural\partightenfactor0

\f0\fs24 \cf0 ## Summary\
This visualization aims at exhibiting visitor inflow and outflow during the Oktoberfest 2017 in Munich. In particular, it displays inflow and outflow for each day of the week (Monday to Sunday) aggregated over the 2 weeks period the Oktoberfest takes place (E.g., data for Monday contains aggregated information on inflow and outflow for the first and second Monday). The basic idea is to show that visitor numbers for the district where the Oktoberfest takes place (District 2) start to increase towards the weekend, peaking either on Friday or Saturday, since I believe the Oktoberfest shows visitor patterns similar to bars and other leisure facilities. Alternatively, Oktoberfest could show a different pattern if we assume that the majority of visitors are tourists. Tourists don\'92t follow a regular week pattern with working from Monday to Friday and going out from Friday to Saturday/Sunday. However, I believe that the majority of visitors are locals from Munich and surrounding areas.\
\
## Information about the dataset\
The data used for the visualization is a collection of mobile phone gps coordinates, sampled every 10 minutes. Those coordinates have been translated into trajectories (raw tracks with a certain start and end destination within the city). Based on algorithms provided by the Open Source Routing Machine (http://project-osrm.org/), as well as custom-made algorithms, trajectories have been refined into routes that snap to the city street network. \
For each district, the number of routes entering and leaving (from a different district vs. to a different district), as well as routes that have their origin and destination in the same district (local), have been calculated. So the data can be used to display aggregated inflow, outflow and local flow for each district. Or alternatively, we can visualize the inflow/outflow to/from a particular district with respect to all other districts, i.e. highlight all districts from which routes end in a district of interest (similarly for the outflow). \
\
- inflow: number of visits entering a particular district (from a different district)\
- outflow: number of visits leaving a particular district (to a different district)\
- local: number of visits with start and end in the same district\
 \
\
\
## Design\
A map of Munich, displaying district boarders as well as the airport area, is used to provide the geographical context. \
\
###initial design decision (version1)\
In the initial design I chose to highlight the district where the Oktoberfest takes place with a different fill color. As such user\'92s attention is directed to the district of interest. A bar chart was used to display the information on inflow and outflow for the district of interest. The name of the district is displayed, as well as the cognate inflow and outflow numbers. \
Furthermore, once the HTML file is loaded, the dashboard will iterate over all weekdays and update accordingly (header will display currently shown day and bar chart will show the respective inflow and outflow numbers). The intention to start with an animation is to immediately embed the user in the \'84story\'93 mode of the dashboard and to explicitly display the change in inflow and outflow over the time frame of weekdays. As previously stated, the goal is to show that visitor inflow/outflow increases with the onset of the weekend.\
After the animation phase buttons for each day of the week appear. Now the user has the opportunity to select the data to be displayed (data subsets for each day). Moreover the user can now also click and select a district of interest to specifically display inflow and outflow for that particular district.\
\
###change in design after feedback 1 \
\
1.A heat map would be a better way to visualize visitor flows for all districts at the same time. \
Now the user has a good overview for all districts and does not have to selectively click through each district for comparison.\
\
2.This is simply an extension of the dataset used for visualization. Inflow and outflow exhibit the number of visitors entering or leaving a particular district from and to another district, respectively. Whereas local represents routes with start and end in the same district. There is no change in design required.\
\
3. Radio buttons  will be incorporated that allow the user to specifically select between each type of visitor flow (inflow, outflow and local). Upon selecting a flow type of interest, the heat map will be updated automatically, which allows a nice a direct feedback to the user.\
\
4. In order to highlight the appropriate district, which hosts the Oktoberfest, as well as other areas of interest (Train Station and Airport), icons have been included with a legend depicting the meaning of each. This allows an easy identification of the main points of interest (Oktoberfest, Train Station, Airport) without unnecessary distracting from the main goal of the dashboard, which is to visualize visitor flows within the course of a week.\
\
Again, the dashboard will start with an animation to \'84pick up\'93 the user and convey the story that visitor flows increase over time, peaking on weekend. Since, the heat map is invoked for a selected type of flow, the animation starts with inflow data. Following animation, the user can change the type of flow data, as well as select a specific day to display. The header has been changed to display the type of flow for a given day without specifying a district name (because the heat map displays data for all districts).\
\
###change in design after feedback 2\
\
1.I decided to simply include a tooltip function together with mouse events to display district names and the corresponding numbers for each flow type if the user hovers over a district. This allows a clean and plain representation and focuses mainly on displaying flow information via the heat map without unnecessary distraction due to additional figure elements. Instead the user can choose to selectively display additional information if need be.\
\
2.To further highlight the district for which the tooltip is being displayed, I decided to change the district boarder size upon mouse hovering. This is an easy way to ensure for the user that the tooltip information displayed actually belongs to that particular district.  Again, this is only a minor addition, which doesn\'92t unnecessary distract from relevant information, but effectively increases overview.\
\
###change in design after feedback 3\
\
1.This means that the dashboard should allow the user to select a district and a type of flow and display flow information in the context of the selected district, i.e. either inflow to selected district from all other districts or outflow from the selected district into all other districts.\
\
I decided to incorporate additional mouse events, which allows the user to select and click a district. Upon selection the district will be highlighted via changing the fill color. Furthermore the heat map will be updated accordingly to represent flow values only for the district selected (only the min and max values that belong to routes with respect to the district selected will be used to define the coloring function). Additionally, the geojson data that stores the information on each district needs to be updated to store flow data with respect to the district selected. Otherwise the geojson contains aggregated flow data for each district.\
So the user is able to select a type of flow data using the radio buttons and then to click on a district of interest. The heat map will be updated, as well as the tooltip information to specifically represent the flow context for the selected district. Additionally, the header will be updated to show the user that the data format has been changed from aggregated type to a district-specific type. Moreover, the radio buttons used to select the type of flow will be hidden only displayed again if the user clicks again to exit the district-specific mode and enter the aggregated heat map mode.\
\
2.One mode should use all data from all days of the week to set the min and max values for the heat map function (default type, as used in all prior heat map versions) . This is the choice of heat map that enables the comparison between the days of the week, allowing to visualize trends over the course of the week (e.g, increase in inflow towards the weekend). However, because some days have a \'84much\'93 lower flow numbers than the day with maximum flow numbers (Saturday), the heat map is not suitable to display nuances for that particular days. Instead of using the aggregated heat map mode (all data used for min and max value setting) the user should be able to turn off the aggregated mode and display a heat map only in the context of the day of interest, i.e. min and max values are set based on data for that particular day only.\
I simply incorporated a toggle ON/OFF switch and named it \'84Aggregated Heatmap\'93. The default value is set to ON, because of the animation over the course of the week. After animation the user can turn off the aggregated mode, which also requires to reselect a day of interest to display the heat map in changed mode.\
\
3. As already stated, trajectories have been translated into routes. This also includes the inference of transport modes (Car, Public Transportation, Walking) for each route. So the statistics displayed will be for each mode of transport present in the dataset. Those statistics are not necessary to convey the designated story, but are still a nice to have extension.\
I decided to use a horizontal bar chart next to the Munich map to visualize each of the aforementioned statistics. The bar charts will also be updated during the animation and display only data for the appropriate day. Those statistics can also serve as a proxy to track any flow changes over the course of a week.\
\
##Feedback and Iteration\
The feedback was collected from colleagues who obviously also have some opinion about what parts of available data should/should not be displayed, as well as design patterns.\
\
### Feedback one\
1. change the chart type to visualize visitor flows\
It has been mentioned that a bar chart only encompasses a small part of the total information available (here, flow data for all districts). So the visualization is very specific, highlighting only one district of interest. It would also be interesting if visitor flow changes during time course of the week for all other districts.\
\
2. include also data from routes that have their origin and destination within the same district (local flow)\
\
3. Allow the user to specifically select the type of flow data to display (either inflow, outflow or local)\
\
4. Show the position of the Oktoberfest on the map\
\
\
###Feedback two\
1. Include information on district names as well as the cognate numbers represented by the heat map\
Since the heat map is a representation for all districts, there is no information on single district names and the cognate numbers for each type of flow data.\
\
2. Highlight for which district the tooltip is being displayed. It may be an issue that at the boarder of \
a district the user moves into another district and sees the wrong information.\
\
\
###Feedback three\
1.Expand the visualization by an additional layer of information and include the ability to display for each district inflow and outflow from other districts and to other districts, respectively. \
\
2.Incorporate a switch that allows to change the heat map type, or more correctly, the sensitivity of the heat map. The reason is that coloring is very weak for frequencies much lower than the most frequent one and, as such, makes it difficult to compare frequency nuances between districts.\
\
3.Add statistics on distance travelled, time travelled and the number of trajectories for each day (aggregated over all trajectories for each day).\
\
\
##Resources\
Trajectories, Routes, Origin-Destination matrix for all city district, as well as route statistics were generated by  custom-made data pipelines and algorithms in python, which also embed the open source routing machine algorithm (OSRM, http://project-osrm.org/). \
Following files contain data on statistics and routes origin-destination matrix:\
\
-in_out_districts_oktoberfest_2017_version1.json (this file is used with index_version1.html)\
-in_out_districts_oktoberfest_2017_version2_3_final.json (this file is used with all other index.html files)\
\
The geojson data of Munich with district resolution was obtained by using the Overpass API (http://overpass-turbo.eu/). Following file contains the processed geojson file that is used to display the map of Munich at district-resolution.\
\
-munich_districts_airport.geojson\
\
Any help with JavaScript/d3 code was obtained via the StackOverflow forum (https://stackoverflow.com/)\
\
Information on how to create a  bar char (https://bost.ocks.org/mike/bar/3/)\
\
##Description on how to navigate using the final html file\
use inflow, outflow, local radio buttons in the upper left corner to select the type of mobility data to be displayed (for more details see Information about the dataset). \
\
use buttons depicting days of the week to select the timeframe of data to be displayed }