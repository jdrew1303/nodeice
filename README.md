<!-- Please do not edit this file. Edit the `blah` field in the `package.json` instead. If in doubt, open an issue. -->


[![nodeice](http://i.imgur.com/NuF1OI0.png)](#)

# nodeice

 [![Support me on Patreon][badge_patreon]][patreon] [![Buy me a book][badge_amazon]][amazon] [![PayPal][badge_paypal_donate]][paypal-donations] [![Ask me anything](https://img.shields.io/badge/ask%20me-anything-1abc9c.svg)](https://github.com/IonicaBizau/ama) [![Version](https://img.shields.io/npm/v/nodeice.svg)](https://www.npmjs.com/package/nodeice) [![Downloads](https://img.shields.io/npm/dt/nodeice.svg)](https://www.npmjs.com/package/nodeice)

> Another PDF invoice generator

[![nodeice](http://i.imgur.com/WnUnlFt.png)](#)

## :cloud: Installation

```sh
$ npm i --save nodeice
```


## :clipboard: Example



```js
const Invoice = require("nodeice");

// Create the new invoice
let myInvoice = new Invoice({
    config: {
        template: __dirname + "/template/index.html"
      , tableRowBlock: __dirname + "/template/blocks/row.html"
    }
  , data: {
        currencyBalance: {
            main: 1
          , secondary: 3.67
        }
      , invoice: {
            number: {
                series: "PREFIX"
              , separator: "-"
              , id: 1
            }
          , date: "01/02/2014"
          , dueDate: "11/02/2014"
          , explanation: "Thank you for your business!"
          , currency: {
                main: "XXX"
              , secondary: "ZZZ"
            }
        }
      , tasks: [
            {
                description: "Some interesting task"
              , unit: "Hours"
              , quantity: 5
              , unitPrice: 2
            }
          , {
                description: "Another interesting task"
              , unit: "Hours"
              , quantity: 10
              , unitPrice: 3
            }
          , {
                description: "The most interesting one"
              , unit: "Hours"
              , quantity: 3
              , unitPrice: 5
            }
        ]
    }
  , seller: {
        company: "My Company Inc."
      , registrationNumber: "F05/XX/YYYY"
      , taxId: "00000000"
      , address: {
            street: "The Street Name"
          , number: "00"
          , zip: "000000"
          , city: "Some City"
          , region: "Some Region"
          , country: "Nowhere"
        }
      , phone: "+40 726 xxx xxx"
      , email: "me@example.com"
      , website: "example.com"
      , bank: {
            name: "Some Bank Name"
          , swift: "XXXXXX"
          , currency: "XXX"
          , iban: "..."
        }
    }
  , buyer: {
        company: "Another Company GmbH"
      , taxId: "00000000"
      , address: {
            street: "The Street Name"
          , number: "00"
          , zip: "000000"
          , city: "Some City"
          , region: "Some Region"
          , country: "Nowhere"
        }
      , phone: "+40 726 xxx xxx"
      , email: "me@example.com"
      , website: "example.com"
      , bank: {
            name: "Some Bank Name"
          , swift: "XXXXXX"
          , currency: "XXX"
          , iban: "..."
        }
    }
});

// Render invoice as HTML and PDF
myInvoice.toHtml(__dirname + "/my-invoice.html", (err, data) => {
    console.log("Saved HTML file");
}).toPdf(__dirname + "/my-invoice.pdf", (err, data) => {
    console.log("Saved pdf file");
});

// Serve the pdf via streams (no files)
require("http").createServer((req, res) => {
    myInvoice.toPdf({ output: res });
}).listen(8000);
```



## :question: Get Help

There are few ways to get help:

 1. Please [post questions on Stack Overflow](https://stackoverflow.com/questions/ask). You can open issues with questions, as long you add a link to your Stack Overflow question.
 2. For bug reports and feature requests, open issues. :bug:
 3. For direct and quick help, you can [use Codementor](https://www.codementor.io/johnnyb). :rocket:


## :memo: Documentation


### `Invoice(options)`
This is the constructor that creates a new instance containing the needed
methods.

#### Params

- **Object** `options`: The options for creating the new invoice:
 - `config` (Object):
   - `template` (String): The HTML root template.
 - `data` (Object):
   - `currencyBalance` (Object):
     - `main` (Number): The main balance.
     - `secondary` (Number): The converted main balance.
     - `tasks` (Array): An array with the tasks (description of the services you did).
     - `invoice` (Object): Information about invoice.
 - `seller` (Object): Information about seller.
 - `buyer` (Object): Information about buyer.

### `initTemplates(callback)`
Inits the HTML templates.

#### Params

- **Function** `callback`: The callback function.

### `toHtml(output, callback)`
Renders the invoice in HTML format.

#### Params

- **String** `output`: An optional path to the output file.
- **Function** `callback`: The callback function.

#### Return
- **Invoice** The `Nodeice` instance.

### `convertToSecondary(input)`
Converts a currency into another currency according to the currency
balance provided in the options

#### Params

- **Number** `input`: The number that should be converted

#### Return
- **Number** The converted input

### `toPdf(options, callback)`
Renders invoice as pdf

#### Params

- **Object|String|Stream** `options`: The path the output pdf file, the stream object, or an object containing:

 - `output` (String|Stream): The path to the output file or the stream object.
 - `converter` (Object): An object containing custom settings for the [`phantom-html-to-pdf`](https://github.com/pofider/phantom-html-to-pdf).
- **Function** `callback`: The callback function

#### Return
- **Invoice** The Invoice instance



## :yum: How to contribute
Have an idea? Found a bug? See [how to contribute][contributing].


## :sparkling_heart: Support my projects

I open-source almost everything I can, and I try to reply everyone needing help using these projects. Obviously,
this takes time. You can integrate and use these projects in your applications *for free*! You can even change the source code and redistribute (even resell it).

However, if you get some profit from this or just want to encourage me to continue creating stuff, there are few ways you can do it:

 - Starring and sharing the projects you like :rocket:
 - [![Buy me a book][badge_amazon]][amazon]—I love books! I will remember you after years if you buy me one. :grin: :book:
 - [![PayPal][badge_paypal]][paypal-donations]—You can make one-time donations via PayPal. I'll probably buy a ~~coffee~~ tea. :tea:
 - [![Support me on Patreon][badge_patreon]][patreon]—Set up a recurring monthly donation and you will get interesting news about what I'm doing (things that I don't share with everyone).
 - **Bitcoin**—You can send me bitcoins at this address (or scanning the code below): `1P9BRsmazNQcuyTxEqveUsnf5CERdq35V6`

    ![](https://i.imgur.com/z6OQI95.png)

Thanks! :heart:


## :dizzy: Where is this library used?
If you are using this library in one of your projects, add it in this list. :sparkles:


 - [`bloggify-shop`](https://github.com/IonicaBizau/bloggify-shop#readme)—eCommerce plugin for Bloggify.

## :scroll: License

[MIT][license] © [Ionică Bizău][website]

[badge_patreon]: http://ionicabizau.github.io/badges/patreon.svg
[badge_amazon]: http://ionicabizau.github.io/badges/amazon.svg
[badge_paypal]: http://ionicabizau.github.io/badges/paypal.svg
[badge_paypal_donate]: http://ionicabizau.github.io/badges/paypal_donate.svg
[patreon]: https://www.patreon.com/ionicabizau
[amazon]: http://amzn.eu/hRo9sIZ
[paypal-donations]: https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=RVXDDLKKLQRJW
[donate-now]: http://i.imgur.com/6cMbHOC.png

[license]: http://showalicense.com/?fullname=Ionic%C4%83%20Biz%C4%83u%20%3Cbizauionica%40gmail.com%3E%20(https%3A%2F%2Fionicabizau.net)&year=2014#license-mit
[website]: https://ionicabizau.net
[contributing]: /CONTRIBUTING.md
[docs]: /DOCUMENTATION.md
