# Pipeline Architecture Diagram
```mermaid

flowchart LR
# Catalogue
CatRaw[Raw Catalogue data] --> CatBronze[Catalogue Bronze]
CatBronze --> CatCheck{Quality Check and Load}
CatCheck -->|Pass| CatSilver[Catalogue Silver]
CatCheck -->|Fail| CatQuarantine[Catalogue Quarantine]
CatQuarantine --> CatClean{Clean Data}
CatClean -->|Pass| CatSilver
CatClean -->|Fail| CatFailed[Failed Clean]
# Circulation
CircRaw[Raw Circulation data] --> CircBronze[Circulation Bronze]
CircBronze --> CircCheck{Quality Check and Load}
CircCheck -->|Pass| CircSilver[Circulation Silver]
CircCheck -->|Fail| CircQuarantine[Circulation Quarantine]
CircQuarantine --> CircClean{Clean Data}
CircClean -->|Pass| CircSilver
CircClean -->|Fail| CircFailed[Failed Clean]
# Events
EventRaw[Raw Events data] --> EventBronze[Events Bronze]
EventBronze --> EventCheck{Quality Check and Load}
EventCheck -->|Pass| EventSilver[Events Silver]
EventCheck -->|Fail| EventQuarantine[Events Quarantine]
EventQuarantine --> EventClean{Clean Data}
EventClean -->|Pass| EventSilver
EventClean -->|Fail| EventFailed[Failed Clean]
# Feedback
FeedRaw[Raw Feedback data] --> FeedBronze[Feedback Bronze]
FeedBronze --> FeedCheck{Quality Check and Load}
FeedCheck -->|Pass| FeedSilver[Feedback Silver]
FeedCheck -->|Fail| FeedQuarantine[Feedback Quarantine]
FeedQuarantine --> FeedClean{Clean Data}
FeedClean -->|Pass| FeedSilver
FeedClean -->|Fail| FeedFailed[Failed Clean]
# Combined Gold Layer
CatSilver --> GoldFact[Gold Fact Tables]
CircSilver --> GoldFact
EventSilver --> GoldFact
FeedSilver --> GoldFact
CatSilver --> GoldSummary[Gold Summary Tables]
CircSilver --> GoldSummary
EventSilver --> GoldSummary
FeedSilver --> GoldSummary
