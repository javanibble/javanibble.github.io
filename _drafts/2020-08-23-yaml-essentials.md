---
layout: post
title: "YAML Essentials"
author: andre
categories: [ yaml ]
tags: [yaml]
image: /assets/images/feature-images/feature-image-yaml-essentials.jpg
description: "This post is an essentials guide about YAML for developers. The YAML syntax is defined with examples on how to use the syntax optimally. Finally, the guide contains links to important YAML websites."
comments: true
---

- Table of Contents
{:toc .large-only}

Originally YAML was an acronym for Yet Another Markup Language since its original purpose was to be a document markup language. The three authors, Clark Evans, Ingy döt Net and Oren Ben-Kiki came together in 2001 realising the projects they worked on have a lot in common. They combined their work into a single project known as YAML, a data serialization language. They renamed YAML to `YAML Ain't Markup Language` which is also a recursive acronym. 

YAML is commonly used for configuration files and in applications where data is being stored or transmitted. YAML has very simplistic data types (scalars, lists, arrays..) and data structures (indentation, dashes, colons ..). The extension of a yaml file can either be `yml` or `yaml`.

## YAML Syntax

### Basic Syntax
The YAML syntax uses indentation for a structure (2 spaces, not tabs), dashes for lists and colons for key-value pairs. No duplicate keys are allowed on the same level. 

Sequences are lists:
```yaml
- Item 1
- Item 2
```

Mappings are key-value pairs:
```yaml
key1: value1
key2: value2
```

A sequence of mappings:
```yaml
- key1: value1
  key2: value2
```

A mapping of mappings:
```yaml
overallkey:
  key1: value1
  key2: value2
```

**Block Style** employs indentation rather than indicators to denote structure. This results in a more human-readable (though less compact) notation, but is also less compact.

```yaml
student: "Joe Soap"
university: 
  city: Pretoria
  country: South-Africa
  name: Tukkies
courses: 
  - "Computer Science"
  - Mathematics
  - Physics
```

**Flow Style** can be thought of as the natural extension of JSON to cover folding long content lines for readability, tagging nodes to control the construction of native data structures, and using anchors and aliases to reuse constructed object instances.  

```yaml
student: "Joe Soap"
university: { name: Tukkies, city: Pretoria, country: South-Africa}
courses: [Computer Science, Mathematics, Physics]
```

### Comments
An explicit comment is marked by a “#” indicator. Comments must be separated from other tokens by white space characters. Comments are a presentation detail and must not be used to convey content information.

```yaml
# This is a comment
students: # This is an inline comment
  - Mark McGwire
  - Sammy Sosa
teachers:
  # This is an inline comment
  - Sammy Sosa
  - Ken Griffey
```

### Scalars
YAML provides three flow scalar styles: double-quoted, single-quoted and plain (unquoted). The double-quoted style is specified by surrounding `"` indicators. This is the only style capable of expressing arbitrary strings, by using `\` escape sequences. The single-quoted style is specified by surrounding `'` indicators. Therefore, within a single-quoted scalar, such characters need to be repeated. The plain (unquoted) style has no identifying indicators and provides no form of escaping.

The scalar represents strings, integers, dates, and other atomic data types.

```yaml
strings:
  - double-quoted: "This is a string value"
  - single-quoted: 'This is a string value'
  - unquoted: This is a string value
nulls: 
  - null
  - ~ 
booleans:
  - true: true          # Other values are { Y, true, Yes, ON  }
  - false: false        # Other values are { n, FALSE, No, off }
integers:
  - canonical: 12345
  - decimal: +12345
  - octal: 0o14
  - hexadecimal: 0xC
floating-point:
  - canonical: 1.23015e+3
  - exponential: 12.3015e+02
  - fixed: 1230.15
  - negative_infinity: -.inf
  - not_a_number: .NaN
timestamps:
  - canonical: 2001-12-15T02:59:43.1Z
  - iso8601: 2001-12-14t21:59:43.10-05:00
  - spaced: 2001-12-14 21:59:43.10 -5
  - date: 2002-12-14
block-notation: | 
  Scalar content can be written in block notation, 
  using a literal style (indicated by `|`) where 
  all line breaks are significant.
folded-style: >
  Scalar content can be written with the 
  folded style (denoted by `>`) where each 
  line break is folded to a space unless it 
  ends an empty or a more-indented line.
```

### Structures
YAML uses three dashes `---` to separate directives from document content. This also serves to signal the start of a document if no directives are present. Three dots `...` indicate the end of a document without starting a new one, for use in communication channels.

```yaml
---
# Directive 1
cluster_name: 'Test Cluster'
num_tokens: 256
listen_address: localhost
---
# Directive 2
cluster_name: 'Production Cluster'
num_tokens: 1024
listen_address: 192.168.10.1
...
```

### Tags
Tags are used for setting a custom URI, setting local tags and setting a data type.

Global tags are URIs and hence globally unique across all applications. The `tag:` URI scheme is recommended for all global YAML tags.

Local tags are specific to a single application. Local tags start with `!`, are not URIs and are not expected to be globally unique. YAML provides a `TAG` directive to make tag notation less verbose

```yaml
%TAG ! tag:javanibble.com,2020:
--- !shape 
- !circle       # tag:javanibble.com,2020:circle
  center: {x: 73, y: 129}
  radius: 7

- !line         # tag:javanibble.com,2020:line
  start: {x: 73, y: 129}
  finish: { x: 89, y: 102 }

- !label        # tag:javanibble.com,2020:label
  start: {x: 73, y: 129}
  color: 0xFFEEBB
  text: Pretty vector drawing.
```

Explicit typing is denoted with a tag using the exclamation point `!` symbol.
* `!!map`  : { Hash table, dictionary, mapping }
* `!!seq`  : { List, array, tuple, vector, sequence }
* `!!str`  : Unicode string
* `!!set`  : { cherries, plums, apples }
* `!!omap` : [ one: 1, two: 2 ] 
* `!!bool` : {true, false}
* `!!null` : {null}
* `!!int`  : Negative numbers (-12), zero (0), positive numbers (34)
* `!!float`: negative numbers (-12.3), zero (0), positive numbers (34.3), infinity (.inf), not a number (.nan)
 
```yaml
!!map {
  ? !!str "sequence"
  : !!seq [ !!str "one", !!str "two" ],
  ? !!str "mapping"
  : !!map {
    ? !!str "sky" : !!str "blue",
    ? !!str "sea" : !!str "green",
  },
}

# This is equal to:
sequence: 
  - one
  - two
mapping: 
  sea: green
  sky: blue
```


### Anchors
An anchor is denoted by the `&` indicator. It marks a node for future reference. An anchored node need not be referenced by any alias nodes. An alias node is denoted by the `*` indicator. The alias refers to the most recent preceding node having the same anchor.

```yaml
- center: &ORIGIN {x: 73, y: 129}
  radius: 7
- start: *ORIGIN
  finish: { x: 89, y: 102 }
- start: *ORIGIN
  color: 0xFFEEBB
  text: Pretty vector drawing.
```


### Indicators
Indicators are characters that have special semantics:
* A `-` hyphen denotes a block sequence entry.
* A `?` question mark denotes a mapping key.
* A `:` colon denotes a mapping value.
* A `,` comma ends a flow collection entry.
* A `[` left bracket starts a flow sequence.
* A `]` right bracket ends a flow sequence.
* A `{` left brace starts a flow mapping.
*	A `}` right brace ends a flow mapping.
* An `#` octothorpe, hash, sharp, pound, number sign denotes a comment.
* An `&` ampersand denotes a node’s anchor property.
* An `*` asterisk denotes an alias node.
* The `!` exclamation is heavily overloaded for specifying node tags.
* A `|` vertical bar denotes a literal block scalar.
* A `>` greater than denotes a folded block scalar.
* An `'` apostrophe, single quote surrounds a single-quoted flow scalar.
* A `"` double quote surrounds a double-quoted flow scalar.
* A `%` percent denotes a directive line.


## YAML Example
The following is an example of an invoice defined in YAML. The structure of the invoice is shown through indentation (2 spaces), the sequence or list of items are denoted by a dash, and finally, the all key-value pairs are denoted by a colon.

```yaml
# Invoice for shipping to the USA.
invoice_nr: '123456'
date: 2020-08-24
company:
  name: The LEGO Group
  address: 
    lines: |
      Højmarksvej 8
      DK-7190 Billund
    country: Denmark
    phone: +45 79 50 60 70
bill_to: &id0001
  contact_person: Amanda Stewart
  client_company: 
    name: Lego World
    address:
      street: 125  Modoc Alley
      city: TERLINGUA
      state: TX 
      zip_code: 79852
ship_to: *id0001
product_items:
  - sku: PI1324A
    description: LEGO NINJAGO Spinjitzu Burst Lloyd - 70687
    quantity: 100
    unit_price: 9,99
    total: 999,00
  - sku: PI1324B
    description: LEGO NINJAGO Spinjitzu Burst Cole - 70685 
    quantity: 100
    unit_price: 9,99
    total: 999,00
tax: 278,00
total: 1998,00
notes: >
  Please only deliver during office hours.
  Ask for Jane Soap at the front desk.
  Alternative contact number is 555-1232
```


## References & Links

* [YAML Official Website][YAML_OFFICIAL]
* [YAML Specification 1.2][YAML_SPEC]
* [YAML Online Editor][YAML_EDITOR]
* [YAML Validator][YAML_LINT]
* [YAML Online Tools][YAML_TOOLS]


## Summary
Congratulations! You have completed the post about the essentials of YAML. Follow me on any of the different social media platforms and feel free to leave comments.

[YAML_OFFICIAL]:https://yaml.org/
[YAML_SPEC]:http://yaml.org/spec/1.2/spec.html
[YAML_EDITOR]:https://onlineyamltools.com/edit-yaml
[YAML_LINT]:http://www.yamllint.com/
[YAML_TOOLS]:https://onlineyamltools.com/