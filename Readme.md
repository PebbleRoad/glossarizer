# Glossarizer

* Reads glossary list from json file or object
* Automatically searches for and marks up glossary terms found on a page with <abbr> attributes
* Supports terms exclusion
* Supports multiple terms
* Replaces TextNodes only
* No involvement from authors

## What it is

A small jquery plugin that automatically marks up glossary terms on a page. The glossary terms can be read from an external json file. When users hover over the link (dashed line), they get to see the glossary definition as a tooltip. 

Tooltips are optional, you can use any third-party tooltips. 

## Why use it

If you are writing content that uses specialist vocabulary or many acronyms you need to mark up content with <abbr> tags so that the definitions can show up as a tooltip. But as authors you really should focus on the writing and not on the marking up content. This is where Glossarizer can help. It automatically marks up the glossary terms on a page by reading off a glossary list.

## How to use it

### 1. Prepare your Glossary Data in a JSON File/Object


    [
      {
        "term": "death, !death star",
        "description": "Cessation of all biological functions"
      },
      {
        "term": "genetic, !genetic testing, genes, DNA",
        "description": "relating to genes or heredity: genetic abnormalities."
      },
      {
        "term" : "creature",
        "description" : "A living being, especially an animal"
      },
      {
        "term" : "subdue",
        "description" : "To conquer and subjugate; vanquish"
      },
      {
        "term" : "replenish",
        "description" : "To fill or make complete again; add a new stock or supply to"
      },
      {
        "term" : "whales",
        "description" : "An inlet of the Ross Sea in the Ross Ice Shelf of Antarctica. It has been used as a base for Antarctic expeditions since 1911."
      }
    ]

### 2. Initialize the plugin


    <script src="//ajax.googleapis.com/ajax/libs/jquery/1/jquery.min.js"></script>
    <script src="tooltip/tooltip.js"></script>
    <script src="jquery.glossarize.js"></script>
    <script>

    $(function(){

      $('.content').glossarizer({
        sourceURL: 'glossary.json',
        callback: function(){
          
          // Callback fired after glossarizer finishes its job
          
          new tooltip();

        }
      });


    });

    </script>



### Plugin Options


    defaults = {
      sourceURL        : '', 
      replaceTag       : 'abbr', 
      lookupTagName    : 'p, ul, a',
      callback         : null,
      replaceOnce      : true,
      replaceClass     : glossarizer_replaced,
      caseSensitive    : false,
      jsonResourcePath : false
    }


## Options

Attribute  | Options                   | Default             | Description
---        | ---                       | ---                 | ---
`sourceURL`   | *string*                  | ``              | JSON file url
`replaceTag`    | *string*                  | `abbr`               | html tag used to replace the matching term
`lookupTagName`   | *string*                     | `p, ul, a`               | Which nodes to search
`replaceOnce`    | *boolean*                  | `true`               | Replace once in a textnode?
`replaceClass`    | *string*                  | `glossarizer_replaced`               | Class name of the replaceTag
`callback`    | *method*                  | `null`               | Completed callback 
`caseSensitive`    | *boolean*                  | `false`               | Match case sensitive
`jsonResourcePath`    | *string*                  | `false`               | JSON rsource path for returned data

## JSON Resource Path

Data may sometimes be returned as an attribute on an object, like: 

    {
      "glossary": {
        "count": 2,
        "terms": [
          {
            "term": "death, !death star",
            "description": "Cessation of all biological functions"
          },
          {
            "term": "genetic, !genetic testing, genes, DNA",
            "description": "relating to genes or heredity: genetic abnormalities."
          }
        ]
      }
    }

The JSON Resource Path option specifies the path in the JSON object to the properly formatted data, in this case, you could provide `['glossary']['terms']`.

## External Methods

Attribute  | Options                   | Example
---        | ---                       | ---     
`destroy`    | *method*                  | `$('.content').glossarizer('destroy');`
