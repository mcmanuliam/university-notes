
```mermaid
erDiagram

user {
}

playlist_battle {
}

playlist_battles_submission {
}

playlist_battle ||--|{ playlist_battles_submission : "recieves" 
user ||--|{ playlist_battles_submission : "submits"
```
