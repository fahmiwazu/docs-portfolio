# :material-database: World Cup Database

## Introduction
In the World Cup project, I'll create a database to store data on World Cup teams, players, and match results. I'll design tables, set up relationships, and run queries to explore stats and results, strengthening my SQL and database skills while organizing tournament data.

## Role
- SQL Developer

## Goals

- **Design a Database Schema**: Create tables to store data about World Cup teams, players, matches, and results.
- **Establish Relationships**: Link tables together, such as associating players with teams and matches with their outcomes.
- **Perform CRUD Operations**: Implement SQL queries to create, read, update, and delete World Cup data.
- **Write Complex Queries**: Develop SQL queries to retrieve specific information, such as top goal scorers, match results, or team performance.
- **Normalize the Database**: Organize data efficiently by normalizing the database to reduce redundancy and ensure data consistency.
- **Enhance SQL and Database Skills**: Strengthen our ability to design and query relational databases, focusing on real-world sports data.

## Resource Overview

??? abstract "Project Directory"
    === "Bash Insert Data"
        ``` Bash title="insert_data.sh"
        #! /bin/bash

        if [[ $1 == "test" ]]
        then
        PSQL="psql --username=postgres --dbname=worldcuptest -t --no-align -c"
        else
        PSQL="psql --username=freecodecamp --dbname=worldcup -t --no-align -c"
        fi

        # Do not change code above this line. Use the PSQL variable above to query your database.

        echo $($PSQL "TRUNCATE TABLE games, teams")

        cat games.csv | while IFS="," read YR RND WIN OPP W_GOAL O_GOAL 
        do
        # echo $YR, $RND, $WIN

        TEAMW=$($PSQL "SELECT team_id FROM teams WHERE name='$WIN'")

        if [[ $WIN != "winner" ]]
        then
            if [[ -z $TEAMW ]]
            then
            IN_W_ID=$($PSQL "INSERT INTO teams(name) VALUES('$WIN')")
            if [[ $IN_W_ID == "INSERT 0 1" ]]
            then
                echo Inserted into winner, $WIN
            fi
            fi
        fi

        TEAML=$($PSQL "SELECT team_id FROM teams WHERE name='$OPP'")

        if [[ $OPP != "opponent" ]]
        then
            if [[ -z $TEAML ]]
            then
            IN_O_ID=$($PSQL "INSERT INTO teams(name) VALUES('$OPP')")
            if [[ $IN_W_ID == "INSERT 0 1" ]]
            then
                echo Inserted into opponent, $OPP
            fi
            fi
        fi

        TEAM_ID_W=$($PSQL "SELECT team_id FROM teams WHERE name='$WIN'")
        TEAM_ID_L=$($PSQL "SELECT team_id FROM teams WHERE name='$OPP'")

        if [[ -n $EAM_ID_W || -n $TEAM_ID_L ]]
        then
            if [[ $YR != "year" ]]
            then
            IN_GAME=$($PSQL "INSERT INTO games(winner_id, opponent_id, winner_goals, opponent_goals, year, round) VALUES('$TEAM_ID_W','$TEAM_ID_L','$W_GOAL','$O_GOAL','$YR','$RND')")
            if [[ $IN_GAME == "INSERT 0 1" ]]
            then
                echo Insert game history, $YR
            fi
            fi
        fi


        done
        ```
    === "PosgreSQL Database Dump"
        ``` SQL title="worldcup.sql"
        --
        -- PostgreSQL database dump
        --

        -- Dumped from database version 12.17 (Ubuntu 12.17-1.pgdg22.04+1)
        -- Dumped by pg_dump version 12.17 (Ubuntu 12.17-1.pgdg22.04+1)

        SET statement_timeout = 0;
        SET lock_timeout = 0;
        SET idle_in_transaction_session_timeout = 0;
        SET client_encoding = 'UTF8';
        SET standard_conforming_strings = on;
        SELECT pg_catalog.set_config('search_path', '', false);
        SET check_function_bodies = false;
        SET xmloption = content;
        SET client_min_messages = warning;
        SET row_security = off;

        DROP DATABASE worldcup;
        --
        -- Name: worldcup; Type: DATABASE; Schema: -; Owner: freecodecamp
        --

        CREATE DATABASE worldcup WITH TEMPLATE = template0 ENCODING = 'UTF8' LC_COLLATE = 'C.UTF-8' LC_CTYPE = 'C.UTF-8';


        ALTER DATABASE worldcup OWNER TO freecodecamp;

        \connect worldcup

        SET statement_timeout = 0;
        SET lock_timeout = 0;
        SET idle_in_transaction_session_timeout = 0;
        SET client_encoding = 'UTF8';
        SET standard_conforming_strings = on;
        SELECT pg_catalog.set_config('search_path', '', false);
        SET check_function_bodies = false;
        SET xmloption = content;
        SET client_min_messages = warning;
        SET row_security = off;

        SET default_tablespace = '';

        SET default_table_access_method = heap;

        --
        -- Name: games; Type: TABLE; Schema: public; Owner: freecodecamp
        --

        CREATE TABLE public.games (
            game_id integer NOT NULL,
            winner_id integer NOT NULL,
            opponent_id integer NOT NULL,
            winner_goals integer NOT NULL,
            opponent_goals integer NOT NULL,
            year integer NOT NULL,
            round character varying(255) NOT NULL
        );


        ALTER TABLE public.games OWNER TO freecodecamp;

        --
        -- Name: games_game_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
        --

        CREATE SEQUENCE public.games_game_id_seq
            AS integer
            START WITH 1
            INCREMENT BY 1
            NO MINVALUE
            NO MAXVALUE
            CACHE 1;


        ALTER TABLE public.games_game_id_seq OWNER TO freecodecamp;

        --
        -- Name: games_game_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
        --

        ALTER SEQUENCE public.games_game_id_seq OWNED BY public.games.game_id;


        --
        -- Name: teams; Type: TABLE; Schema: public; Owner: freecodecamp
        --

        CREATE TABLE public.teams (
            team_id integer NOT NULL,
            name character varying(255) NOT NULL
        );


        ALTER TABLE public.teams OWNER TO freecodecamp;

        --
        -- Name: teams_team_id_seq; Type: SEQUENCE; Schema: public; Owner: freecodecamp
        --

        CREATE SEQUENCE public.teams_team_id_seq
            AS integer
            START WITH 1
            INCREMENT BY 1
            NO MINVALUE
            NO MAXVALUE
            CACHE 1;


        ALTER TABLE public.teams_team_id_seq OWNER TO freecodecamp;

        --
        -- Name: teams_team_id_seq; Type: SEQUENCE OWNED BY; Schema: public; Owner: freecodecamp
        --

        ALTER SEQUENCE public.teams_team_id_seq OWNED BY public.teams.team_id;


        --
        -- Name: games game_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.games ALTER COLUMN game_id SET DEFAULT nextval('public.games_game_id_seq'::regclass);


        --
        -- Name: teams team_id; Type: DEFAULT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.teams ALTER COLUMN team_id SET DEFAULT nextval('public.teams_team_id_seq'::regclass);


        --
        -- Data for Name: games; Type: TABLE DATA; Schema: public; Owner: freecodecamp
        --

        INSERT INTO public.games VALUES (33, 394, 395, 4, 2, 2018, 'Final');
        INSERT INTO public.games VALUES (34, 396, 397, 2, 0, 2018, 'Third Place');
        INSERT INTO public.games VALUES (35, 395, 397, 2, 1, 2018, 'Semi-Final');
        INSERT INTO public.games VALUES (36, 394, 396, 1, 0, 2018, 'Semi-Final');
        INSERT INTO public.games VALUES (37, 395, 398, 3, 2, 2018, 'Quarter-Final');
        INSERT INTO public.games VALUES (38, 397, 399, 2, 0, 2018, 'Quarter-Final');
        INSERT INTO public.games VALUES (39, 396, 400, 2, 1, 2018, 'Quarter-Final');
        INSERT INTO public.games VALUES (40, 394, 401, 2, 0, 2018, 'Quarter-Final');
        INSERT INTO public.games VALUES (41, 397, 402, 2, 1, 2018, 'Eighth-Final');
        INSERT INTO public.games VALUES (42, 399, 403, 1, 0, 2018, 'Eighth-Final');
        INSERT INTO public.games VALUES (43, 396, 404, 3, 2, 2018, 'Eighth-Final');
        INSERT INTO public.games VALUES (44, 400, 405, 2, 0, 2018, 'Eighth-Final');
        INSERT INTO public.games VALUES (45, 395, 406, 2, 1, 2018, 'Eighth-Final');
        INSERT INTO public.games VALUES (46, 398, 407, 2, 1, 2018, 'Eighth-Final');
        INSERT INTO public.games VALUES (47, 401, 408, 2, 1, 2018, 'Eighth-Final');
        INSERT INTO public.games VALUES (48, 394, 409, 4, 3, 2018, 'Eighth-Final');
        INSERT INTO public.games VALUES (49, 410, 409, 1, 0, 2014, 'Final');
        INSERT INTO public.games VALUES (50, 411, 400, 3, 0, 2014, 'Third Place');
        INSERT INTO public.games VALUES (51, 409, 411, 1, 0, 2014, 'Semi-Final');
        INSERT INTO public.games VALUES (52, 410, 400, 7, 1, 2014, 'Semi-Final');
        INSERT INTO public.games VALUES (53, 411, 412, 1, 0, 2014, 'Quarter-Final');
        INSERT INTO public.games VALUES (54, 409, 396, 1, 0, 2014, 'Quarter-Final');
        INSERT INTO public.games VALUES (55, 400, 402, 2, 1, 2014, 'Quarter-Final');
        INSERT INTO public.games VALUES (56, 410, 394, 1, 0, 2014, 'Quarter-Final');
        INSERT INTO public.games VALUES (57, 400, 413, 2, 1, 2014, 'Eighth-Final');
        INSERT INTO public.games VALUES (58, 402, 401, 2, 0, 2014, 'Eighth-Final');
        INSERT INTO public.games VALUES (59, 394, 414, 2, 0, 2014, 'Eighth-Final');
        INSERT INTO public.games VALUES (60, 410, 415, 2, 1, 2014, 'Eighth-Final');
        INSERT INTO public.games VALUES (61, 411, 405, 2, 1, 2014, 'Eighth-Final');
        INSERT INTO public.games VALUES (62, 412, 416, 2, 1, 2014, 'Eighth-Final');
        INSERT INTO public.games VALUES (63, 409, 403, 1, 0, 2014, 'Eighth-Final');
        INSERT INTO public.games VALUES (64, 396, 417, 2, 1, 2014, 'Eighth-Final');


        --
        -- Data for Name: teams; Type: TABLE DATA; Schema: public; Owner: freecodecamp
        --

        INSERT INTO public.teams VALUES (394, 'France');
        INSERT INTO public.teams VALUES (395, 'Croatia');
        INSERT INTO public.teams VALUES (396, 'Belgium');
        INSERT INTO public.teams VALUES (397, 'England');
        INSERT INTO public.teams VALUES (398, 'Russia');
        INSERT INTO public.teams VALUES (399, 'Sweden');
        INSERT INTO public.teams VALUES (400, 'Brazil');
        INSERT INTO public.teams VALUES (401, 'Uruguay');
        INSERT INTO public.teams VALUES (402, 'Colombia');
        INSERT INTO public.teams VALUES (403, 'Switzerland');
        INSERT INTO public.teams VALUES (404, 'Japan');
        INSERT INTO public.teams VALUES (405, 'Mexico');
        INSERT INTO public.teams VALUES (406, 'Denmark');
        INSERT INTO public.teams VALUES (407, 'Spain');
        INSERT INTO public.teams VALUES (408, 'Portugal');
        INSERT INTO public.teams VALUES (409, 'Argentina');
        INSERT INTO public.teams VALUES (410, 'Germany');
        INSERT INTO public.teams VALUES (411, 'Netherlands');
        INSERT INTO public.teams VALUES (412, 'Costa Rica');
        INSERT INTO public.teams VALUES (413, 'Chile');
        INSERT INTO public.teams VALUES (414, 'Nigeria');
        INSERT INTO public.teams VALUES (415, 'Algeria');
        INSERT INTO public.teams VALUES (416, 'Greece');
        INSERT INTO public.teams VALUES (417, 'United States');


        --
        -- Name: games_game_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
        --

        SELECT pg_catalog.setval('public.games_game_id_seq', 64, true);


        --
        -- Name: teams_team_id_seq; Type: SEQUENCE SET; Schema: public; Owner: freecodecamp
        --

        SELECT pg_catalog.setval('public.teams_team_id_seq', 417, true);


        --
        -- Name: games games_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.games
            ADD CONSTRAINT games_pkey PRIMARY KEY (game_id);


        --
        -- Name: teams teams_name_key; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.teams
            ADD CONSTRAINT teams_name_key UNIQUE (name);


        --
        -- Name: teams teams_pkey; Type: CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.teams
            ADD CONSTRAINT teams_pkey PRIMARY KEY (team_id);


        --
        -- Name: games fk_games_opponent; Type: FK CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.games
            ADD CONSTRAINT fk_games_opponent FOREIGN KEY (opponent_id) REFERENCES public.teams(team_id);


        --
        -- Name: games fk_games_winner; Type: FK CONSTRAINT; Schema: public; Owner: freecodecamp
        --

        ALTER TABLE ONLY public.games
            ADD CONSTRAINT fk_games_winner FOREIGN KEY (winner_id) REFERENCES public.teams(team_id);


        --
        -- PostgreSQL database dump complete
        --
        ```
    === "Query Challange"
        ``` Bash title="queries.sh"
        #! /bin/bash
        
        PSQL="psql --username=freecodecamp --dbname=worldcup --no-align --tuples-only -c"
        
        # Do not change code above this line. Use the PSQL variable above to query your database.
        
        echo -e "\nTotal number of goals in all games from winning teams:"
        echo "$($PSQL "SELECT SUM(winner_goals) FROM games")"
        
        echo -e "\nTotal number of goals in all games from both teams combined:"
        echo  "$($PSQL "SELECT SUM(winner_goals + opponent_goals) FROM games")"
        
        echo -e "\nAverage number of goals in all games from the winning teams:"
        echo  "$($PSQL "SELECT AVG(winner_goals) FROM games")"
        
        echo -e "\nAverage number of goals in all games from the winning teams rounded to two decimal places:"
        echo  "$($PSQL "SELECT AVG(winner_goals)::NUMERIC(10,2) FROM games")"
        
        echo -e "\nAverage number of goals in all games from both teams:"
        echo  "$($PSQL "SELECT AVG(winner_goals + opponent_goals) FROM games")"
        
        echo -e "\nMost goals scored in a single game by one team:"
        echo  "$($PSQL "SELECT MAX(winner_goals) FROM games")"
        
        echo -e "\nNumber of games where the winning team scored more than two goals:"
        echo  "$($PSQL "SELECT COUNT(*) FROM games WHERE winner_goals > 2")"
        
        echo -e "\nWinner of the 2018 tournament team name:"
        echo  "$($PSQL "SELECT name FROM teams INNER JOIN games ON teams.team_id=games.winner_id WHERE round='Final' AND year=2018")"
        
        echo -e "\nList of teams who played in the 2014 'Eighth-Final' round:"
        echo  "$($PSQL "SELECT name FROM teams INNER JOIN games ON teams.team_id=games.winner_id OR teams.team_id=games.opponent_id WHERE round='Eighth-Final' AND year=2014 ORDER BY name")"
        
        echo -e "\nList of unique winning team names in the whole data set:"
        echo  "$($PSQL "SELECT DISTINCT(name) FROM teams INNER JOIN games ON teams.team_id=games.winner_id ORDER BY name")"
        
        echo -e "\nYear and team name of all the champions:"
        echo  "$($PSQL "SELECT year, name FROM teams INNER JOIN games ON teams.team_id=games.winner_id WHERE round='Final' AND ( year=2018 OR year=2014) ORDER BY year")"
        
        echo -e "\nList of teams that start with 'Co':"
        echo  "$($PSQL "SELECT name FROM teams WHERE name LIKE 'Co%' ")"
        ```

## Attachment

- **Project workspace**: [Build a World Cup Database on freeCodeCamp](https://www.freecodecamp.org/learn/relational-database/build-a-world-cup-database-project/build-a-world-cup-database)
- **GitHub Repository**: [World Cup Database Repository](https://github.com/fahmiwazu/fcc-rdb-worldcupdb)

