# Assignment 1
## Domains

1. **Watching sports:** As a sports fan and athlete myself, beyond just watching games, I’m interested in the data side: stats, trends, and insights that go deeper than highlights. I often find myself wishing for better ways to visualize, compare, or personalize sports data so that it’s easier to connect what I’m seeing on the field with the underlying numbers.
2. **Listening to music:** As a music listener, I want to visualize my music taste and dive deeper into the kinds of music that I like. I often wish that I could learn more about an artist from their Spotify profile (age, hometown, education, etc). I would also want to know the different genres of music that I listen to and identify areas to explore.
3. **Playing/following chess:** As a chess player, I want to visualize my Elo over time and see the success rate that I have for different openings against other openings. I often want to keep track of the games that I’ve played and visualize trends with my overall playing. It would also be valuable to compare my performance with peers or track the progress of my team, since chess is both an individual and community activity. This would allow chess players to make data-driven decisions about how to go about improving.
4. **Student productivity:** As a student, I want a way to keep track of my current tasks and view my study habits.
5. **Leading a student club:** As a student club leader, I want to keep track of attendance for members of my group, as well as see information about them.
6. **Planning for travel:** As a traveler, I want to keep track of trip specific details like hotel prices, flight prices, activity availability, all in a centralized place.
7. **Going to college:** As an incoming college student, I want to know what items are the most worth for me to purchase for my room /  general use.
8. **Choosing a dorm:** As an incoming (or current) college student, I want to see what the culture is like from dorms on my campus. I'd want to hear the honest experiences of residents of the dorm, not just what the school puts online.
9. **Playing video games:** As a video game player, I want to see what games are coming out soon and see what content creators are playing games that I like.
10. **Keeping up with the latest SWE news:** As a software engineer or student studying computer science, I want a centralized place to view the latest industry trends and see what experienced engineers.

## Problems
### Watching sports
1. (SELECTED) **Information overload:** As a sports fan, highlights and data are posted for every sport, every team, and every player. If I could present data in a way that is more digestible for sports fans at all levels, that would be a success. I think this would be an interesting problem to tackle from a UI/UX perspective. The data processing would be relatively simple, but might depend heavily on external integrations.
2. **Personalization:** The core of this project would be a complex recommendation system, which does not seem in the scope of this class.
3. **Connecting data to the game:** Tying statistics to specific video moments would be technically challenging because it is a multimedia problem. The bulk of the work would be finding the correct APIs to use, and also seems outside the scope of this class.


### Listening to music
1. **Limited artist context:** Providing data about artists seems more like a data problem instead of a software engineering problem.
2. **Genre exploration:** I think this wouldn't work for a similar reason to the sports personalization problem.
3. (SELECTED) **Music taste visualization:** Transforming raw music listening data into a dynamic interface seems like an interesting challenge. If this would fall into the "elaborate data visualization" category, I am happy to pick another category.

### Playing/following chess
1. (SELECTED) **Game reviews:** Current chess game reviews are very low-level (move based). A higher level game review would be an interesting problem space to work on. This project would allow for multiple users on the platform, interacting with each other's profiles and viewing each other's games. The second idea could also be merged into this one.
2. **Tracking performance:** There are already tools that do this, and the idea is quite simple to implement, so I don't think it would be a very interesting problem to solve.
3. **Following professional players:** The bulk of this project would be filtering chess news data for relevant information to display, which is outside the scope of this class. This could probably be done as a newsletter instead of a web project.

## Stakeholders
### Watching sports - Information overload
1. **Casual fans** (people who watch sports time to time) want a way to follow their favorite teams and players without being overwhelmed. Impact: they would save time scrolling through highlights and become more engaged with their favorite teams/players.
2. **Analysts** (can be from media or news) care about how to engage fans with data and would benefit from better tooling to determine which insights to talk about. Impact: they will have more engagement with their content if it more focused to a specific fanbase.
3. **Sports teams** will have another platform to gain fans from. Impact: more attention from fans, more merchandise bought, tickets sold, etc.


### Listening to music - Music taste visualization
1. **Everyday listeners** want to understand their own listening habits. Impact: users can discover their listening habits on the platform and branch off *on their own* to different genres and artists.
2. **Streaming platforms** want to know the engagement with different genres and artists on their platform so they know who to promote. Impact: more engagement with advertisements.
3. **Artists** gain more dedicated fans, as listeners refine their music tastes based on data. Impact: artists can grow their fanbase as well as view the location of their audiences to strategically plan concerts and tours.

### Playing chess - Game reviews
1. **Amateur players** want higher-level insights (that aren't move-by-move analysis) to improve more efficiently. Impact: users will improve at a faster pace and don't need to spend their time understanding complex chess analysis. They will also save time extracting insights from their games.
2. **Chess coaches** could benefit from having aggregated results to guide practice sessions and assign readings / matches to study. Impact: coaches will have more successful teams and teachings that are more catered to each individual student.
3. **Chess platforms** could adapt this methodology of review and gain users as a result. Impact: more traffic on chess sites, and the barrier to chess analysis lowers, allowing more players to improve at the game.

## Evidence
### Watching sports - Information overload
1. [Challenges and Limitations of Sports Analytics: What We Still Don’t Know](https://medium.com/%40data-overload/challenges-and-limitations-of-sports-analytics-what-we-still-dont-know-d6e1d34a445a) explores how a lack of data standardization can make it difficult to compare and analyze data across different sports.
2. [How Data Analytics Boosts Fan Engagement in Sports](https://builtin.com/articles/data-analytics-fan-engagement-sports) explores how current sports dashboards fall short to meet the growing need for easy to understand insights.
3. [The application of big data analytics in sports as a tool for personalized fan experience, operations efficiency, and fan engagement strategy](https://www.researchgate.net/publication/388383788_The_application_of_big_data_analytics_in_sports_as_a_tool_for_personalized_fan_experience_operations_efficiency_and_fan_engagement_strategy) explores how big data and digestible data presentation can optimize fan engagement.
4. [The Role of Data in Enhancing Fan Engagement for Sports Teams](https://www.fancompass.com/blog/2024/8/2/the-role-of-data-in-enhancing-fan-engagement-for-sports-teams) explores how demographic data, behavioral data, and engagement data are the building blocks for digestible feeds.
5. [The Digital Arena: How Big Data is shaping the Fan Experience](https://www.sportsvenue-technology.com/articles/the-digital-arena-how-big-data-is-shaping) explores how raw performance data is overwhelming and must be made meaningful for fans.
6. [Data science in sports analytics: A review of performance optimization and fan engagement](https://www.researchgate.net/publication/377863761_Data_science_in_sports_analytics_A_review_of_performance_optimization_and_fan_engagemen) explores how sports data is very abundant, but the main challenge is presenting it in a user-friendly way (kind of too heavy on the visualization aspect).
7. [Evaluation function](https://en.wikipedia.org/wiki/Evaluation_function) explores how, in general, complexity can hinder comprehension.
8. [In Sports, Not Everything That Counts Can Be Counted. Why Sports Data and Analytics Can't Replace Human Intuition](https://www.turningdataintowisdom.com/the-role-of-data-and-analytics-in-sports-finding-the-balance-with-human-analysis/) explores how analytics often introduces unwanted complexity.
9. [Genius Sports](https://www.geniussports.com/) is a company that offers data visualization tools for sports. However, their target audience is teams and players. They have great visualizations for a lot of advanced data, but could benefit for something more fan-focused and not as advanced. 

### Listening to music - Music taste visualization
1. [Visual Analyses of Music History: A User-Centric Approach](https://arxiv.org/abs/1703.07534) confirms how personalized versions of listening history confirm user experience. 
2. [Interactive Visualization for Music Rediscovery](chrome-extension://efaidnbmnnnibpcajpcglclefindmkaj/https://pdfs.semanticscholar.org/6f49/8457e03e5d186330719d6fbdb4486095c7cd.pdf) explores how an interactive interface can help solidify music taste understanding and is backed by user tests.
3. [Music Visualizer Market Size, Share, Growth, and Industry Analysis](https://www.businessresearchinsights.com/market-reports/music-visualizer-market-115408) shows the growth of the music visualization market. The compound annual growth rate of this industry is 27.8%, which I believe (?) is very high, proving that there are demand for this type of tool.
4. [Spotify Wrapped Marketing Strategy: Data Storytelling & Creating a Viral Cultural Phenomenon](https://nogood.io/blog/spotify-wrapped-marketing-strategy/) describes what a success Spotify Wrapped (a music taste visualization tool) is. Over 227 million users interacted with this feature in 2023.
5. [Share of people who share their Spotify Wrapped on social media among Spotify users in the United States as of December 2022](https://www.statista.com/statistics/1385158/spotify-wrapped-social-media/) is another Spotify Wrapped based website, showing how 14% of Spotify users poster their Wrapped on social media.
6. [last.fm](https://www.last.fm/) is a comparable. It is notably inaccurate with data, which is it's main drawback.
7. [receiptify](https://www.receiptify.us/) is a comparable that displays most listened to songs, artist, etc. for the past month. However, it lacks robustness and flexibility in the data that is displayed.
8. [Obscurify](https://obscurify.us/) is a comparable that benchmarks your artist preferences against over 120 million other Spotify listeners, making it highly accurate in quantifying your music taste uniqueness.

### Playing chess - Game reviews
1. [Computer evaluation numbers on Chess.com (like +2.25)](https://support.chess.com/en/articles/8379354-computer-evaluation-numbers-on-chess-com-like-2-25) is a forum post that explains how current game review features, like advantage, is difficult to understand for novice/beginner players.
2. [Detailed Critique of New Game Review](https://www.chess.com/forum/view/site-feedback/detailed-critique-of-new-game-review-110227953) is a user forum that explains how the current [chess.com](chess.com) UI for game review needs to zoom out and focus less on a move-by-move basis
3. [Game review is now being limited](https://www.reddit.com/r/chess/comments/1fg2622/game_review_is_now_being_limited/) is a Reddit thread that discusses how higher-level review is being put behind a paywall, which makes users frustrated.
4. [Cheating in Online Chess](https://en.wikipedia.org/wiki/Cheating_in_online_chess) entails that current chess tooling need more generalization to reach a larger fanbase.
5. [ChessBase](https://en.wikipedia.org/wiki/ChessBase) is a database of chess games, but explains how average users lack access to high-level summary tools. 
6. [Wired: Best Chess Apps](https://www.wired.com/story/best-chess-apps/) explains how platforms like Lichess and chess.com offer analysis, but mainly have basic move-by-move and no higher-level. This shows that there is a niche for higher-level chess review
7. [Elo rating system](https://en.wikipedia.org/wiki/Elo_rating_system) explains how the chess elo system is fundamentally flawed and how players should focus on improving their play rather than focus on just their rating. To me, this tool would be a good solution to focusing on improving rather than some arbitrary number.
8. [Game review/analyze - game auto store - can I avoid/disable it ?](https://www.chess.com/forum/view/site-feedback/game-review-analyze-game-auto-store-can-i-avoid-disable-it) is another chess forum discussing how they want to view the critical points of the game, rather than the entire game move-by-move. This demonstrates need for higher-level game analysis.
9. [chess.com](chess.com) is the main comparable for this project. The main friction is that users would need to export their games from chess.com to my platform, which might be too high of an activation energy. chess.com has pretty much dominated the game review space for advance analysis, but I still think there is a niche for more beginner players.

## Features
### Watching sports - Information overload
1. **Preference selector:** This would be the main area for a user to input their favorite teams and players. They will also be able to input their level of understanding of each sport, allowing the platform to adjust accordingly and present appropriate information.
2. **Recent games summarizer:** This would be the main part of the platform. Based on the level of understanding indicated by the user, the past $n$ games of the player or team would be summarized at the appropriate complexity. Only the most relevant statistics would be displayed, ensuring that the user is able to easily extract insights from the data.
3. **Contextual information:** Users would be able to increase the complexity of data shown coupled with explanations for more advanced topics and statistics. This allows the user to steadily grow their knowledge of the sport.

### Listening to music - Music taste visualization
1. **Genre heatmap:** A color-coded map of genres the user listens to the most/least. This would give the user a very clear visual of their taste.
2. **Timeline:** A user can see their listening trends over time, displayed on a timeline. This highlights the shifts in their favorite artists and moods.
3. **Friend profiles and similarity reports:** Users will be able to follow their friends on the platform to follow their listening trends. This can spark real conversation and allow users to establish common interests with others. Users will be able to generate similarity reports with other users on the platform to compare and contrast taste

### Playing chess - Game reviews
1. **Game input:** Users will be able to import games into the database with information like: moves in the game, opening played, opening played against, game result. This game data is what will drive the entire review system, and is the most important feature of the platform.
2. **Peer/coach review mode:** Users will be allowed to share games and trends with friends or coaches who can highlight key lessons. This incentivizes users to collaborate with their peers and coaching to improve at a faster rate. Players can build a strong community and gain practice partners through this feature. Players and coaches will also have profiles that display games and favorite strategies, with external links to these strategies. Users will always be able to explore new strategies and openings they haven't seen before.
3. **High level insights:** Users will be able to see data like a momentum graph, which is a high level way of displaying advantage throughout the course of a chess game. Ideally, there will be other ways of making engine analysis more digestible, but this seems more like a data visualization problem. However, some level of visualization is required to identify trends in the data.