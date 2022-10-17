# Runtime API drift 

To detect Zombie and Shadow APIs, you want to analyze with the API Clarity analyzer.

## Rules 

|name_id                                                     |severity|title                                                       |description                                                 |mitigation                                                                 |
|------------------------------------------------------------|--------|------------------------------------------------------------|------------------------------------------------------------|---------------------------------------------------------------------------|
|GENERAL_DIFF                                                |error   |GENERAL_DIFF                                                |General diff: a general diff has been detected              |Please update the spec accordingly.                                        |
|ZOMBIE_DIFF                                                 |error   |ZOMBIE_DIFF                                                 |Zombie: a deprecated API has been detected                  |Please update clients to stop using deprecated APIs.                       |
|SHADOW_DIFF                                                 |error   |SHADOW_DIFF                                                 |Shadow: an undocumented API has been detected               |Please add the API in the spec.                                            |
