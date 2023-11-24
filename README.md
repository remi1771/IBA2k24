# IBA2k24
International Basketball Association. A Basketball Sim Game inspired by NBA 2K and other sport games' lack of features and greed.

Features and notes to future self:

The Database contains the following tables
Please note, you'll see that most stats and tendencies are missing, this is because I'm debating where I want to place them, lol.



Players Table:
		Contains information about players and mainly references correspondant to that player such as Name, JerseyID, FaceID, etc. It doesn't containt to which team it belongs because it doesn't lock players on a 1:1 ratio with teams. Players can have more than 1 team, this is due to many reasons, mainly to avoid having to duplicate players when Dream Teams, or All-Time teams, or National Teams, are needed. For example Michael Jordan would be both on the 1992 Dream Team, and 1992 Chicago Bulls, and (if 1992 where his best season) All Time Chicago Bulls, and 1992 East All Stars, and 1992 All-NBA Team, and the 1992 All-Defensive Team. So instead of having 6 duplicate 92' Michael Jordan's, Teams can just assign 92'MJ to their roster. Some duplication system might be needed if 2 teams (with the same player) play against each other but either A) This happens in quickplay so we could just create a player, paste all 1992MJ Data to it and continue, because stats won't be relevant after the game is quit or B) This happens in Season (Maybe some type of showmatch 1992 All-Defensive vs 1992 Champions Chicago Bulls) and in that case one team would have priority (in the beforementioned case the bulls), but no 2 players would be the same for inmerssions sake.

  I don't quite now where to put the stats yet, should it be inside the players table? A different table? I don't think a different table makes sense, because it's unlikely 2 players that are not the same share the same identical stats but, who knows.

  Some notes on data. Order has 4 Options albeit more could be added: F.Last or First Last or L. First or Last First. Nickname is not the same as Jersey_Nickname. Nickname, is more for the commentary and other panels. Birthdate doesn't have a Year (it could be birthday now that I think about it). YearBorn is separate, so as to calculate the Age the player has. 
  
  Year refers to the Year the player represents, so for example Michael Jordan's 1992 Season Year would be 1992. This is quite distinct from other sport games, because it basically creates a player for every year the player played, this is to basically allow the option of having all possible seasons inside the game (at the cost of maybe a terabyte of data lol), so you could play 1992 Bulls vs 1993 Bulls ;). Year is also used to calculate age (Year-YearBorn=Age)

  Draft has 3 aspects, Year Drafted, Round Drafted, Pick Drafted. This only applies to leagues that have drafts (NBA, WNBA, PBA, CBA, B.League, ABA, etc.)

 Childhood Team refers to his childhood team, the team he watched/liked growing up, this can be NULL. Preferred Team follows similar basis, and affects decision making on CareerMode
 
Play for Winner, Play for Money, Play for Fun, Play for Time, and Loyalty are all sliders for CareerMode

Players have two "From:" aspects: Nationality, and College. Whenever College is not NULL it'll be selected.

BodyID fetches his BodyStats basically, CommentaryId does the same with the phrases associated with him, JerseyID same with jersey.

Jersey Table:
    - Jersey ID
    - Jersey Nickname
    - Jersey Number
    - Shirt Tucked or Untucked
    - Shirt Length
    - Short Length
    - Sock Type
    - Shoes
    - Sponsor
    - YearIntroduced

Body Table:
    - BodyID (Primary Key)
    - FaceID (Foreign Key)
    - Height
    - Wingspan
    - Muscle
    - Weight
    - ShoulderSize
    - BicepSize
    - ForearmSize
    - BellySize
    - PecSize
    - PecShape
    - ButtSize
    - ButtShape
    - LegSize
    - GastrocnemiusSize
    - HandSize
    - HasTattoos (Boolean)

Face Table:
    - FaceID
    - Mural ID
    - Portrait ID
    - Action Shot ID

Commentary Table:
    - CommentaryId (Primary Key)
    - Phrases (List of PhraseKeys as a comma-separated string)

Phrases Table:
    - PhraseKey (Primary Key)
    - Phrase (Text of the commentary phrase with placeholders for dynamic content)

Teams Table:
    - TeamID (Primary Key)
    - FranchiseID (To connect all same franchise teams in some way)
    - Name
    - Year
    - Year of Origin
    - City
    - Arena
    - Overall
    - ChampionshipsWon
    - ConferenceFinals
    - LastPlayoffAppearance
    - DebutDate
    - JerseyID
    - OverridesPreferredJersey
    - CommentaryID
    - Players (List of PlayersID sepparated by comma)

Coaches Table:
    - CoachID (Primary Key)
    - Name
    - Birthdate
    - YearsActive
    - ChampionshipsWon
    - CommentaryId

Referees Table:
    - RefereeID (Primary Key)
    - Name
    - Birthdate
    - YearsActive
    - CommentaryId
    - TechnicalFoul_Tendency
    - DriveFoul_Tendency
    - PostFoul_Tendency
    - OverTheBack_Tendency
    - Travelling_Tendency
    - ReachinFoul_Tendency
    - BlockingFoul_Tendency
    - JerseyID (Foreign Key referencing Jerseys table)

Games Table:
    - GameID (Primary Key)
    - SeasonID (Foreign Key referencing Seasons table)
    - TeamAID (Foreign Key referencing Teams table)
    - TeamBID (Foreign Key referencing Teams table)
    - CourtID (Foreign Key referencing Courts table)
    - RefereeID (Foreign Key referencing Referees table)
    - Date
    - Round (PreSeason/Season/1st round/2nd round/ Conference Semi-Finals/Conference Finals/Finals/Post Season/Special)
    - TeamAScore
    - TeamBScore
    - MVP (Foreign Key referencing PlayerID)

Courts Table:
    - CourtID (Primary Key)
    - CourtName
    - Location
    - SeatingCapacity

Transactions Table:
    - TransactionID (Primary Key)
    - PlayerID (Foreign Key referencing Players table)
    - CoachID (Foreign Key referencing Coaches table)
    - TeamFromID (Foreign Key referencing Teams table)
    - TeamToID (Foreign Key referencing Teams table)
    - TransactionType
    - Date
    - Details

Seasons Table:
    - SeasonID (Primary Key)
    - Year
    - RegularSeasonStartDate
    - RegularSeasonEndDate
    - PlayoffStartDate
    - PlayoffEndDate
    - Games (List of GameID sepparated by comma)
    - Awards (List of AwardID sepparated by comma)

Awards Table:
    - AwardID (Primary Key)
    - Name
    - Description
    - PlayerID (Foreign Key referencing Players table)
    - SeasonID (Foreign Key referencing Seasons table)

Game Details Table:
    - GameDetailID (Primary Key)
    - GameID (Foreign Key referencing Games table)
    - PlayerID (Foreign Key referencing Players table)
    - PlayerRating (Points + (OffensiveRebounds + Blocks + Steals+Assists)*2 / PlaysParticipated) 
    - FG
    - FGA
    - FT
    - FTA
    - 2PT
    - 2PA
    - 3Pt
    - 3PA
    - 4PT
    - 4PA
    - 5PT
    - 5PA
    - Blocks
    - Steals
    - Rebounds
    - Defensive Rebounds
    - Offensive Rebounds
    - Assists
    - MinutesPlayed
    - PlusMinus

Leagues Table:
