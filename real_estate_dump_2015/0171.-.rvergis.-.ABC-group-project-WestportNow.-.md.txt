ABC-group-project-WestportNow
=============================

The DatabaseActivity lets you create and delete the database and dump to the log stream information about the fake content created.  Buttons allow you to exercise the two APIs described below, with the results sent to the log.

The fake content includes 3 fake authors and 40 fake articles. The "subject" fields are taken from the real website, e.g. "Sport" and "Real Estate."

Look at the button handlers in DatabaseActivity to see how to access the fake database.

The Article class is where all the interesting stuff happens. See these two functions:

static public ArrayList<Article> getArticlesNoOlderThan(int timestamp, String subjectFilter) {
 // Return a list of articles from a database fetch.
 // To support newspaper sections (sports, finance, real estate, etc.), the subjectFilter, if not
 // null, causes only articles with a matching subject to be returned. (RSS "Subject" == "Section")

static public ArrayList<String> getSubjects() {
 // Return a list of subjects, to populate the list of sections the user might choose among.

As Ron identifies new database requirements, please let me know and I'll implement them. Separately, I'll
work on fetching, parsing, and storing real articles from the RSS feed in a background task or service.
Until that's ready, this fakery should suffice for front-end development.
