# LTL to CZK converter Safari extension #

This simple extension converts price information on visited websites. It searches the document for a price in Lt (Lithuanian Litas, LTL) and converts the price to Kč (Czech Crowns, CZK). A hard-coded exchange rate 7.5 Kč for 1 Lt is used.

The extension is written in CoffeeScript.

## **Not** supported features: ##

 * Real exchange rate loaded and cached from a bank.
 * LTL instead of just Lt.
 * Prices without a space between the value and the currency.
 * Other currencies than LTL and CZK.
 * Opposite way conversion (CZK to LTL).
 * Converting prices in ALT and TITLE attributes.
 * Converting prices in dynamically loaded content.

 * etc. etc.

# Side note #

A motivation to writing this extension was to be able to browse lithuanian e-shops and real estate servers without having to recalculate every single price information to the native currency of my country. Hence I wanted to try developing a working (even though just really simple) Safari extension.
