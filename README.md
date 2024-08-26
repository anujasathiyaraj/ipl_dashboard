
![image](https://github.com/user-attachments/assets/8a115c2d-58af-4565-878a-aa6554fbe92f)


![image](https://github.com/user-attachments/assets/bb5fbdd9-bee6-49bf-82f8-62a8f158dbd6)


![image](https://github.com/user-attachments/assets/c93b8635-361d-48e6-9a53-eef2e63e0cc8)


## Measures used
Total Runs = SUM(fact_bating_summary[runs])


Batting Strike min 60 balls = 
    VAR TotalRuns = [Total Runs]
    VAR TotalBalls = [Total Balls Faced]
    VAR SeasonsOver60Balls =
        CALCULATE(
            COUNTROWS(
                FILTER(
                    VALUES(dim_match_summary[Year]),
                    dim_match_summary[Year] >= 2021 &&
                    dim_match_summary[Year] <= 2023 &&
                    [Total Balls Faced] >= 60
                )
            )
        )
    RETURN
        IF(
            NOT ISFILTERED(dim_match_summary[Year]),
            IF(
                SeasonsOver60Balls = 3,
                DIVIDE(TotalRuns, TotalBalls, 0) * 100,
                BLANK()
            ),
            IF(
                SeasonsOver60Balls > 0,
                DIVIDE(TotalRuns, TotalBalls, 0) * 100,
                BLANK()
            )
        )


Batting Average min 60 balls = 
VAR TotalRuns = [Total Runs]
VAR TotalOuts = [Total Inning Dismissed]
VAR SeasonsOver60Balls =
    CALCULATE(
        COUNTROWS(
            FILTER(
                VALUES(dim_match_summary[Year]),
                [Total Balls Faced] >= 60
            )
        ),
        dim_match_summary[Year] >= 2021 && dim_match_summary[Year] <= 2023
    )
RETURN
    IF(
        NOT ISFILTERED(dim_match_summary[Year]),
        IF(
            SeasonsOver60Balls = 3,
            DIVIDE(TotalRuns, TotalOuts, 0),
            BLANK()
        ),
        IF(
            [Total Balls Faced] >= 60,
            DIVIDE(TotalRuns, TotalOuts, 0),
            BLANK()
        )
    )
 



Boundary% = 
VAR TotalRuns = [Total Runs]
VAR BoundaryRuns = [Boundary_Runs_m]
VAR SeasonsOver60Balls =
    CALCULATE(
        COUNTROWS(
            FILTER(
                VALUES(dim_match_summary[Year]),
                [Total Balls Faced] >= 60
            )
        ),
        dim_match_summary[Year] >= 2021 && dim_match_summary[Year] <= 2023
    )
RETURN
    IF(
        NOT ISFILTERED(dim_match_summary[Year]),
        IF(
            SeasonsOver60Balls = 3,
            DIVIDE(BoundaryRuns,TotalRuns,0),
            BLANK()
        ),
        IF(
            [Total Balls Faced] >= 60,
            DIVIDE(BoundaryRuns,TotalRuns,0),
            BLANK()
        )
    )
 



Total Wickets = Sum(fact_bowling_summary[wickets])


Dot Balls % Min 60 Balls = 
    VAR TotalDotBalls = [Dot Balls]
    VAR TotalBalls = [Total Balls Bowled]
    VAR SeasonsOver60Balls =
        CALCULATE(
            COUNTROWS(
                FILTER(
                    VALUES(dim_match_summary[Year]),
                    [Total balls bowled] >= 60
                )
            ),
                    
            dim_match_summary[Year] >= 2021 &&
            dim_match_summary[Year] <= 2023
        )
    RETURN
        IF(
            NOT ISFILTERED(dim_match_summary[Year]),
            IF(
                SeasonsOver60Balls = 3,
                Divide([Dot Balls], [Total Balls Bowled],0),
            BLANK()
        ),
        IF(
            [Total balls bowled] >=60, 
            Divide([Dot Balls], [Total Balls Bowled],0),
            BLANK()
        )
        )



Economy Rate min 60 Balls = 
VAR TotalRunsC = [Total Runs Conceded]
VAR TotalBallsB = [Total Balls Bowled]
VAR SeasonsOver60Balls =
    CALCULATE(
        COUNTROWS(
            FILTER(
                VALUES(dim_match_summary[Year]),
                [Total Balls Bowled] >= 60
            )
        ),
        dim_match_summary[Year] >= 2021 &&
        dim_match_summary[Year] <= 2023
    )
RETURN
    IF(
        NOT ISFILTERED(dim_match_summary[Year]),
        IF(
            SeasonsOver60Balls = 3,
            Divide(TotalRunsC, TotalBallsB,0) * 6,
            BLANK()
        ),
        IF(
            [Total Balls Bowled] >= 60,
            DIVIDE(TotalRunsC, TotalBallsB,0) *6,
            BLANK()
        ))
