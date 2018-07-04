# WorthIT

WorthIT can help you decide if you can work in a location and find affordable housing there. First, you can search for available jobs and see the average salary for that position. Then, you can see the rental housing options, including number of bedrooms and locations, that you can get at various percentages of that salary. This can help you decide if it is worth it for you to accept a job offer and how much you will need to spend to find a rental that matches your needs.

![animated gif showing start screen of app](animated-dropdown.gif)

## Get started

The app is deployed on https://zrowe.github.io/WorthIt/.

1. Choose a job title from the drop-down list.
2. View job openings from the GitHub Jobs site that match the title. Click the link to view the original posting, get more details about it, and apply.
3. View the average salary in San Francisco for that job title, as compiled by Glassdoor.
4. View the types of rental housing options in San Francisco and neighboring cities that are within 30-, 40-, and 50-percent of that salary.
5. Choose a different job title to see how the salary affects what you can get for the money.

### Installation

To run locally for development purposes, clone this repository and open `index.html`.

## Technology

- [AJAX](https://en.wikipedia.org/wiki/Ajax_(programming)) to query job board and housing APIs.
- HTML, CSS, and [Bootstrap (version 4)](https://getbootstrap.com/docs/4.0/getting-started/introduction/) to build the user interface and make the website mobile-responsive.
- [Firebase](https://firebase.google.com/) to cache housing data for quicker access.
- JavaScript and [jQuery](https://jquery.com/) to code the app and interact with user interface elements.

## Contributors

- [Jack Fang](https://github.com/jackfang415)
- [Rhonda Glennon](https://github.com/rmglennon)
- [Jose Perez](https://github.com/jperez650)
- [Paul Rowe](https://github.com/zrowe)
- [Akhil Sompalli](https://github.com/sompaak)

## License

This project is licensed under the MIT License; see the [LICENSE](LICENSE) file for details.

## Acknowledgments and data credits

- Job postings are from the [GitHub Jobs API](https://jobs.github.com/api).
- Salary estimates are provided by [Glassdoor](https://www.glassdoor.com/Salaries/index.htm) and based on salaries submitted anonymously to Glassdoor, as of February 2018.
- Rental housing data is from the [Quandl API](https://www.quandl.com/data/ZILLOW-Zillow-Real-Estate-Research) for Zillow Real Estate Research, as of February 2018.
- San Francisco background image is from [orboloops9 on imgur](https://imgur.com/gallery/Kzyb3BE).
- Thanks to Amber and Jerome for feedback and review.
