dm
==

Digital MarketPlaces - Real Estate Dev


About the 'dist' folder, PHP layout modules, wget, localhost, gh-pages for QA and the migrate bash script

'dist' - This folder contains the compiled, concatenated and otherwise near final output of the layouts and their resources. We use grunt to run several tasks that then copy the output into this folder. 

'PHP Layouts/modules markup' - In addition to resources and flat html pages for each layout, in this folder you can find the each module and their parts split into their own php file or module. We use the frameset.php, along with a URL variable (home, serp, property-listings, neighborhood) to display an HTML complete layout. All markup updates for the layouts and modules need to be done in their corresponding php module to avoid inconsistent markup. The php modules/layout are separated into folders that match their function or roles similar to BDC SVN repo.

'wget' - Install wget, I recommend using homebrew to install it (brew install wget)

'localhost' - Because we are creating the markup for the page using wget you'll need to setup PHP run through localhost and either move your copy of the repo symlink it to where you have set locahost to live.

'gh-pages' - The final markup that will be available for QA lives on the gh-pages branch of the repo. The contents of gh-pages is only made up of the resources in the dist folder (js, styles, fonts, images) and the HTML page layouts that are created by the migrate bash script.

'migrate' - This script will copy a set of resources from the dist folder to a temporary folder outside your repo, use wget to copy the markup of the layouts into straight HTML, naming them after their corresponding layout (frameset?page-type=articles will be used to create articles.html in this folder). It will then checkout the gh-pages branch, copy the contents (overriding) of the temporary folder into the pages branch; git pull, commit and push the contents to the repo before swithcing back to the master branch.
