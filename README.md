# Live IPL Dashboard

### Dashboard Link : https://app.powerbi.com/groups/me/reports/f8f88fd8-9d57-49b5-abc3-310d9ca6ca19/ReportSection?experience=power-bi

## Problem Statement

This IPL Dashboard is designed to provide real-time tracking and visualization of match statistics, offering a comprehensive overview of ongoing games. It addresses the need for cricket enthusiasts, analysts, and stakeholders to stay updated with live match developments efficiently.

By leveraging this dashboard, users can:

- Monitor Live Scores and Statistics : Gain immediate access to live scores, player performances, and key match statistics, allowing for an in-depth understanding of the game as it unfolds.

- Analyze Team and Player Performance : Evaluate the performance of teams and individual players through various metrics such as runs scored, wickets taken, and strike rates, which are crucial for strategic decision-making.

- Identify Trends and Patterns : Recognize patterns and trends in player performances and match outcomes, aiding analysts in making data-driven predictions and insights.

- Engage and Enhance Viewer Experience : Enhance the viewing experience for fans by providing interactive and visually appealing data representations, making the game more engaging and enjoyable.

- Support Strategic Decisions for Teams : Assist team management and coaching staff in making real-time strategic decisions based on live data, improving the chances of success during the match.

Delighted to share that I've crafted one of the most robust and innovative dashboard to date, focusing on the exhilarating realm of IPL.

Data Integration: Learned how to connect and integrate live cricket score APIs into this Power BI dashboard, allowing for real-time match data updates effortlessly. Dashboard Design: Advanced techniques for designing visually appealing and informative dashboards tailored for cricket enthusiasts. Real-Time Updates: Implemented real-time data refresh functionalities to ensure this dashboard provides up-to-the-minute cricket scores. Interactivity: This dynamic dashboard not only provides real-time updates on IPL live scores but also offers comprehensive insights into player performance, team statistics, points table and match analysis. Optimization: Optimized this dashboard for peak performance and optimal user experience, ensuring swift data retrieval and smooth navigation for the users. Excited to showcase the power of data visualization in revolutionizing sports analytics.

## Steps followed 

- Step 1 : Get the API from https://rapidapi.com/cricketapilive/api/cricbuzz-cricket.
- Step 2 : Open power query editor & run the query to fetch the data from Cricbuzz server.
       
        let
           apiUrl = "https://cricbuzz-cricket.p.rapidapi.com/series/v1/7607",
           apiKey = "50a6166de9msh2a5d646f7fd7a31p1c91eajsnbabb2f3bd67d",
           apiHost = "cricbuzz-cricket.p.rapidapi.com",
    
           headers = [
                  #"X-RapidAPI-Key" = apiKey,
                  #"X-RapidAPI-Host" = apiHost
           ],

           getApiData = (url as text, headers as record) =>
           let 
               response = Web.Contents(url, [Headers=headers]),
               jsonResponse= Json.Document(response)
           in
               jsonResponse,
    
           apiData = getApiData(apiUrl, headers)

        in
           apiData
        
    Obtained data from the Cricbuzz API:

    ![Screenshot 2024-06-05 105713](https://github.com/Abtg08/Live-IPL-Dashboard/assets/87989296/799cb61b-b0cf-4911-9d5f-56a48bc2bb40)

        
- Step 3 : Expanded the "list" coloumn to get the "Matches List".
- Step 4 : Emphasised on using minimal API calls to make the dashboard and thus used reference of single API call to  fect all other relevant data from the server.
- Step 5 : Used the following query in the "Advanced Editor" to fetch the live score form the Cricbuzz server:
       
        let
            Match_ID= Text.From(Live_Matches_ID{0}[Match ID]),
            apiUrl = "https://cricbuzz-cricket.p.rapidapi.com/mcenter/v1/"& Match_ID &"/scard",
            apiKey = "50a6166de9msh2a5d646f7fd7a31p1c91eajsnbabb2f3bd67d",
            apiHost = "cricbuzz-cricket.p.rapidapi.com",
    
            headers = [
                    #"X-RapidAPI-Key" = apiKey,
                    #"X-RapidAPI-Host" = apiHost
            ],

            getApiData = (url as text, headers as record) =>
                    let 
                        response = Web.Contents(url,[Headers=headers]),
                        jsonResponse = Json.Document(response)
                    in
                        jsonResponse,
    
            apiData = getApiData(apiUrl, headers)
        
        in
            apiData
        
- Step 6 : Live match data was obtained through this.
    ![Screenshot 2024-06-05 110218](https://github.com/Abtg08/Live-IPL-Dashboard/assets/87989296/c01acb48-bc52-47bf-b5f7-6d18699b8a3c)

- Step 7 : Expanding the coloumns in this list we obtained multiple details about the ongoing match.

- Step 8 : Filters were added for the fields "Team ID", "Batting Team Name", "Bowling Team Name" && their respective ID's.

- Step 9 : The next step was to fetch the "Live Team Score", "Live Batsman Score", "Live Bowler Score" and "Players Information".

- Step 10 : With all the relevant data, the dashboard was set up. It contained two fileds: 
    
                Current Batting Team 
                Current Bowling Team
    
    During the First Inning the scorecard is set to show who won the toss on the Bowling Team tile and during the Second Innings the Total Score made by the first team will be displayed.

    ![Screenshot 2024-06-05 111956](https://github.com/Abtg08/Live-IPL-Dashboard/assets/87989296/6d2f528c-a31f-4ab6-aa64-54307af4c7f6) 

- Step 11 : Then the following deatils were extracted and added onto the dashboard:

    ![Screenshot 2024-06-05 112217](https://github.com/Abtg08/Live-IPL-Dashboard/assets/87989296/d36476fe-3b79-461c-8666-9523d1b46d7c)


    ![Screenshot 2024-06-05 112238](https://github.com/Abtg08/Live-IPL-Dashboard/assets/87989296/3e4e1c17-81d9-42ee-9fce-29b250a31e76)


    ![Screenshot 2024-06-05 112301](https://github.com/Abtg08/Live-IPL-Dashboard/assets/87989296/8e2dc3c2-a9d7-4949-9d71-2164d8d19015)

    ![Screenshot 2024-06-05 112323](https://github.com/Abtg08/Live-IPL-Dashboard/assets/87989296/c0991cf1-d3be-44f9-9fdb-fd84248ad40f)

- Step 12 : In the next step, I created the Points Table section to show the current standing of each team. To achive this I used the points table API from Cricbuzz. Using it I extracted the following coloumns from the data: 
    - Status
    - Team
    - Team Name
    - Captain Image
    - Total Matches Played
    - Won
    - Lost
    - Points 

    ![Screenshot 2024-06-05 112437_1](https://github.com/Abtg08/Live-IPL-Dashboard/assets/87989296/f8eb63d0-31e0-4878-8e85-2cbcf42f47ec)

- Step 13 : DAX measures were created to obtain fields like Current Batsman, Current Bowler, Current Batsman Image, Current Captian Image, Current Run Rate, Required Run Rate. All of these can be viewd in detail through the pbix file in the repositorty.

- Step 14: A "Home Page" was created and buttons were used to link the "Home Page", "Live Score" and "Points Table".

- Step 15: Uploaded the entire Dashboard to PowerBI Service.

# Snapshot of Dashboard (Power BI Service)

![Screenshot 2024-06-05 112353](https://github.com/Abtg08/Live-IPL-Dashboard/assets/87989296/52433144-2023-4573-b953-9c46fc1a90b9)

![Screenshot 2024-06-05 112414](https://github.com/Abtg08/Live-IPL-Dashboard/assets/87989296/8359b8bb-2e67-43f6-897a-ed5a09e01306)

![Screenshot 2024-06-05 112437](https://github.com/Abtg08/Live-IPL-Dashboard/assets/87989296/3519414f-9522-4845-9d94-33af664aeabe) 
