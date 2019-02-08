# SHACL CI Testing Showcase
## About This Repository
This is a repository demonstrating the use of Travis CI together with the Shapes Constraint Language (SHACL) for
automatic validation of ontology projects. Despite being common in many parts of the software industry, to the current
date development of ontologies still lacks an easy to use testing framework. The lack of proper quality assurance can
easily lead to the unnoticed introduction of various errors
[(example)](http://www.semantic-web-journal.net/system/files/swj1825.pdf), some of which could be avoided by means of
automated testing. This repository aims to be a first step towards solving that issue. We provide a single `.travis.yml`
file anyone could easily add to their repository to get started quick and without any hassle. Using the [SWEET Ontology
of Scientific Units](https://github.com/ESIPFed/sweet), we also give an example of some tests, the results of which can
be seen by checking out the commit history.

## About SHACL
SHACL is a language designed for the validation of RDF graphs against a set of constraints. Its *closed world reasoning*
model, adherence to the *Unique Name Assumption (UNA)*, and interoperability with OWL makes it an ideal tool for
ontology verification. Our script makes use of the [TopBraid SHACL API](https://github.com/TopQuadrant/shacl/) to
perform these validations.
To learn more about SHACL and how it relates to OWL, take a look at [this article](http://spinrdf.org/shacl-and-owl.html).
The official specification can be found [here](http://spinrdf.org/shacl-and-owl.html).

## Getting Started
Setting up the CI for your own project is simple and can be done following these steps:
1. Sign up with [Travis CI](https://travis-ci.com/) and activate it for your repository.
1. Add the `.travis.yml` file to your repository.
1. Point the `SHAPES_DIR` variable to the folder containing your tests.
1. Point the `DATA_FILE` variable to the file containing your ontology. Currently, only single files are supported.
1. (Optional) Set the `UNCLUTTER` variable according to your preference. Normally, the validation report will contain
   lots of less relevant information such as all prefixes used or all the RDF triples involved. Printing all these
   information can significantly clutter the output, especially when multiple test files are involved, and thus harm
   readability. If the `UNCLUTTER` variable is set, the script will use the pcregrep utility to perform a multi-line
   regular expression search on the report, trying to filter out only the relevant part. This feature has however not
   been extensively tested and there might be cases where it behaves erratically. If it seems to be causing problems,
   please try turning it off and consider opening an issue.

That's it! You should be ready to use Travis CI with your ontology project now.

## Using a Binary SHACL Distribution
The script relies on newly introduced features (i.e., error codes) of the SHACL API which are currently not present in
the binary releases on the [Maven Central Repository](http://central.maven.org/maven2/org/topbraid/shacl/), and
therefore has to do the time-consuming build itself. However, it is also possible to provide your own binary. To do so,
use the `.travis.yml` file from the `shacl-binary` branch and follow these steps:
1. Clone the [TopBraid SHACL API](https://github.com/TopQuadrant/shacl/) to your hard drive.
1. Execute `mvn package` at the root of the project (requires Maven to be installed and set up).
1. Upload the `shacl-(version)-bin.zip` from the `target` folder to a place of your choice.
1. Adjust the `SHACL_URL` variable to point to your uploaded file (the `SHACL_VERSION` variable is not required and can
   be omitted).

## Licensing
The files from this repository (excluding the contained SWEET Ontology) are released into the public domain in order to
encourage and make their use as straightforward and simple as possible. You are free to copy, modify, and share your
modified versions without any restrictions. While being appreciated, attributions are not required. Please consult the
[LICENSE](https://github.com/p-conrad/shacl-ci-testing/blob/master/LICENSE) file for more information.

## Authors
This project has been created as a university project by Peter Conrad with guidance from [Jan Martin
Keil](https://github.com/jmkeil), Friedrich Schiller University Jena.
