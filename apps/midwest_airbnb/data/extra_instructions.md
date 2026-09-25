# Extra Instructions

Rules the LLM follows when it writes SQL for `listings`.

- `price` is the nightly price in U.S. dollars. When the user asks what something costs, use `price` and round money to whole dollars in the answer.

<!-- Add more rules below (Assignment 05 asks for at least three). Good candidates:
     `host_is_superhost` and `instant_bookable` are the text values 't' and 'f',
     not booleans; how to match a city name the user types; how to search `name`
     case-insensitively; and whether to ignore rows whose `review_scores_rating`
     is NULL when averaging ratings. -->

- `city` may be typed by the user in any capitalization (e.g., "chicago", "Chicago", "CHICAGO"). When filtering or matching on `city`, use LOWER(city) = LOWER('user input') so the match works regardless of case.

- `name` can be searched by the user with any capitalization (e.g., "loft", "Loft", "LOFT") and may only be a partial match to the full listing title. When filtering or matching on `name`, use LOWER(name) LIKE LOWER('%user input%') with % wildcards so partial, case-insensitive matches are found.

- Some listings have NULL for review_scores_rating because they've never been reviewed. AVG(review_scores_rating) already ignores NULL values automatically, so no special filtering is needed for the math. However, when reporting an average rating, also mention how many listings that average is based on using COUNT(review_scores_rating) (which only counts non-NULL ratings) — do not use COUNT(*), since that would count unreviewed listings too and mislead the user.
