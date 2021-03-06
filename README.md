# HackItAll Elimination Round

This is a code implementation of a vending machine designed to allow the sale
of Avira products to students. For this implementation we chose to use Python.

![UI screenshot](https://github.com/vladirares/HackItAll/blob/master/UI.png)

## Implementation

This vending machine implementation allows users to use two different payment
methods: cash or card. If the cash option was selected different types of 
currency can be inserted until the owed value has been inserted. The machine
will also give back change if need be. If the card option was selected then the
user will have to select his items and input his card pin. If the pin was 
correct the purchase will go through. If this is not the case items will be
returned to stock.
To keep track of what is purchased during a transaction aand to make sure no
errors arrise, the machine uses a virtual basket to which selected items are
added in their respective quantities.

## Classes

The following classes were implemented in the design of this app:

* **Product**: defines the properties of each item on sale
	* *Name*: the get(*self*) and set(*self, name*) methods in this category
				set and return the name of a product
	* *Price*: this method category is split into a get(*self*) and a 
				set(*self, price*) method that update and retrieve the given
				price of a product

* **Cash**: defines the methods used in cash payments
	* On initialization of an object, a dictionary containing each type of 
	currency that can be used. This dictionary will be used to keep track of
	all the currency inserted into the machine
	* *insertMoney(self, amount)*: adds inserted currency to the dictionary
	* *getChange(self, currentcredit, totalcartvalue)*: gives back owed change
	* *getMoney(self)*: returns the total ammount of currency inserted

* **Card**: defines methods used for card payments
	* On initialization of an object, a preset card balance and pin are set up
	(this is done only for the purpose of this implementation)
	* *getFunds(self)*: returns card balance
	* *updateFunds(self, price)*: updates balance following a purchase
	* *checkFunds(self, price)*: checks to determine if the selected items are 
	affordable based on card balance
	* *checkPin(sef, givepin)*: checks to see if inputted pin is correct

* **VendingMachine**: this class is the core of the machine; it is set up as a
	singleton class so there can only be one object of this type the class 
	also defines a basket to keep track of items the user wishes to aquire
	* On initialization, this class sets up all of the available products, creates a dictionary with the prices of each item as well as a dictionary
	with the number of products contained in the machine
	* *insertProduct(product)*: adds a product to virtual basket
	* *getBasket()*: retrieves all the items stored in the virtual basket
	* *getBasketPrice()*: returns the total value of items in the virtual 
	basket
	* *clearBasket()*: clears the virtual basket
	* *getCredit(self)*: returns credit available to the user
	* *getNo< product_name >(self)*: returns the existing amount for each
	product
	* *getPrice< product_name >(self)*: returns the price for each item

* **Button(object)**: this class defines a button object for use in UI
	* On initializition the button is place at it's respective coordinates on
	the screen, it's size is defined, it gets given a name and an image to
	display
	* *draw(self,screen)*: this method is called every frame to have the button
	redrawn
	* *event_handler(self, event)*: this method handles what happens when the
	button is clicked

* **PaymentButton(Button)**: this class defines the button type for the buttons
	used in selecting the payment methods
	* On initialization the same setup is performed as for the standard button 
	class defined above
	* *event_handler(self, event)*: this method handles what happens when the
	button is clicked

* **Text**: defines the label-style objects used to display text
	* On initialization the font style and size, text and position are set up
	* *draw(self, screen)*: this method is used to redraw and update the label
	every frame

* **PriceText(Text)**: this defines the labels that are used for displaying UI
	text
	* On initialization these labels have the same setup as defined in the 
	generic text label class 

* **CoinsText(Text)**: this defines a clickable label that is used to display 
	each increment of currency accepted
	* On initialization these labels use the same setup as defined in the
	generic text label class the only difference being that these posses a 
	value and are clickable
	* *event_handler(self,event)*: this method handles what happens when the 
	labels are clicked

* **TextButton(Text)**: this defines a clickable label for each product
	* On initialization these labels use the same setup as defined in the
	generic text label class the only difference being that these posses a 
	value and are clickable
	* *event_handler(self,event)*: this method handles what happens when the 
	labels are clicked

* **Plot**: this class defines the way statistics are kept and plots are done 
	(the plotting file starts out with some base test values; these are only
	relevant in the context of this implementation; new values are added as
	transactions are made)
	* *getPlot(self, array)*: this method plots out the total machine revenue
	* *getProductsPlot(self,fileName)*: this method creates the plots for each
	of the product statistics sets

## Statistics

The way we chose to keep track of product sale statistics by storing the total 
amount of money accumulated in the vending machine and the revenue generated by
each transaction. This revenue is categorised by each product to allow Avira to
easily keep track of which product was the most favoured and which brought the
least profits.

All data is stored in a special file to allow for easy exporting and a plot 
creating tool was also implemented using the `matplotlib` library in Python.
This allows for easy visualisation of all data.

The following is an example of the way we display individual product statistics

![Plot screenshot 1](https://github.com/vladirares/HackItAll/blob/master/plot1.png)

The following is an example of the way total machine revenue is displayed

![Plot screenshot 2](https://github.com/vladirares/HackItAll/blob/master/plot2.png)

## Libs

The following Python libraries have been used:
* `matplotlib` for plotting
* `pygame` for UI development

## Usage

To run the following program you are required to download the entire 
repository and run `python Main.py`. You are required to have installed
`pygame`, `matplotlib` and `python3.7.x`

## Authors

Jelea Vladimir-Rares, Pescaru Tudor-Mihai, Petrescu Cosmin
