# Text Generator Plugin

**Language Namespace :** `com.dslfoundry.plaintextgen`

This extension is an alternative text generator for MPS, using the standard model to model generation mechanisms (node macros, loop macros, property macros, etc.) to generate plain text, as opposed to MPS's programmatic text generation.

It allows you to:

- generate directly to plain text without modeling your generation target language
- target multiple text formats in the same generator run
- create multiple textgens that obey generator priority rules

The plugin also enables copy/pasting an existing piece of text and parameterizing parts of this text using macros.

For fine-grained control of whitespaces and indent-characters, the plaintextflow extension is available. It can be imported as a separate language (extending the plaintextgen language), so it doesn't disrupt existing plaintextgen functionality.

## Quickstart

The quickest way to install the plaintextgen plugin is to add it from the JetBrains plugins repository:

- in MPS, select `File` -> `Settings` -> `Plugins` -> `Browse repositories...`
- search for `plaintextgen`
- press `Install`

After installation, add `com.dslfoundry.plaintextgen` to the `Used Languages` of your generator (`main@generator` model) and create a `TextgenText` template in your generator.
There's a test language in this repository that demonstrates this language.

# Presentations and tutorials

A [tutorial on plaintextgen](https://dslfoundry.com/plaintextgen-tutorial/) is available on the [DSLFoundry blog](https://dslfoundry.com/).

A presentation that was held at the 27 February 2019 meeting of [MPS Power Users Group](https://mps-community.nl/power-users-group/) that can be found at the [DSLFoundry MPS-teaching repository](https://github.com/DSLFoundry/mps-teaching/blob/master/Plaintextgen.pdf).

## Main features
* Group and layout your content using horizontal, vertical, and indented collections
* Split plain text into various cells to apply MPS generator macros to them
* Paste unstructured text from a buffer to MPS. The structure of this text (indentations, new lines, tabs) will be automatically analyzed and converted into a `TextgenText` structure which you can then parameterize at your convenience.

## Advantages of this plugin over the default textgen
In short, this plugin brings MPS -> plaintext connectivity in a pretty usable way to MPS.

* Text generation can be part of your normal generator chain and can thus have a place in the generator priorities
* The language looks similar to the MPS editor language, which helps you to structure/layout your text, including indentation
* Different use cases are accommodated:
 * Pasting in larger amounts of text from the clipboard and parametrizing some of it
 * Making text from scratch and parameterizing some of it

## Differences to standard textgen mechanism
The standard textgen approach assumes that you model your target language (e.g. XML, or C in mbeddr) as an MPS language with all its concepts. Concept textgens provide a simple translation from concept to text. This approach is great for language extensibility, but requires that you model concepts of your target language, which sometimes is too large an investment.

This plugin allows you to write a text template and fill in the gaps using standard macros.
For example: You generate from your DSL directly to VHDL, but VHDL has not yet been modeled in MPS.

Additionally, because text is now also an MPS model, all standard generator mechanisms (including reductions and generator priorities) apply. This is not the case for the default textgens, which are only triggered after all model to model transformations are complete.
Also, this approach enables you to implement the textgen as a language extension (and therefore define multiple textgens for the same concept).
