# Inheritance

## Single Table Inheritance

Pros:
* does not require SQL joins to get records from one class
* easy to modify base class or change inheritance hierarchy
* easy to keep unique primary key between types

Cons:
* not optimal disk storage usage

```ruby
# Table name: players
#  id              primary key
#  name            string       not null
#  type            string       not null
#  club_name       string
#  batted_average  integer
#  goals_average   integer
class Player
  attribute :name
end

class FootballPlayer < Player
  attribute :club_name
end

class CricketPlayer < Player
  attribute :batted_average
end

class Bowler < CricketPlayer
  attribute :goals_average
end
```

## Concrete Table Inheritance

Pros:
* does not require SQL joins to get records from one class

Cons:
* hard to modify base class or change inheritance hierarchy
* hard to keep unique primary key between all tables

```ruby
class Player
  attribute :name
end

# Table name: football_players
#  id          primary key
#  name        string       not null
#  club_name   string
class FootballPlayer < Player
  attribute :club_name
end

# Table name: cricket_players
#  id              primary key
#  name            string       not null
#  batted_average  integer
class CricketPlayer < Player
  attribute :batted_average
end

# Table name: bowlers
#  id              primary key
#  name            string       not null
#  batted_average  integer
#  goals_average   integer
class Bowler < CricketPlayer
  attribute :goals_average
end
```

## Class Table Inheritance

Pros:
* simplest solution - each class has own table

Cons:
* can require many SQL joins to get records from one class

```ruby
# Table name: players
#  id    primary key
#  name  string       not null
class Player
  attribute :name
end

# Table name: football_players
#  id         primary key
#  player_id  integer      not null
#  club_name  string
class FootballPlayer < Player
  attribute :club_name
end

# Table name: cricket_players
#  id              primary key
#  player_id       integer      not null
#  batted_average  integer
class CricketPlayer < Player
  attribute :batted_average
end

# Table name: bowlers
#  id                 primary key
#  player_id          integer      not null
#  cricket_player_id  integer      not null
#  goals_average      integer
class Bowler < CricketPlayer
  attribute :goals_average
end
```
