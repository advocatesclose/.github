

# ADVOCATES CLOSE CORPORATION

Advocates Close (the "Company") is a company that develops technology for use by corporate attorneys. 

## Research and Experimentation

  - Business Component: A product that offers to clients the ability to prepare a registration statement and all documents required to be attached as exhibits thereto in respect of a SPAC IPO in 15 minutes or less.
  - This product has been in development for 48 months, 18 days and 4 hours as of this writing.
  - Development has required the creation of numerous other business components.

## Business Components

The following business components have been developed.

### Document Components

#### I/O 

  [Document Reading Component]()

  [Document Formatting Component]()
  
  [Document Comparison Component]()
  
  [Document Persistence Component]()
  
  [Document Printing Component]()

### Content

#### Templating

  [Creating a template]()

  [Reading from a template]()

  [Writing to a template]()

  [Operating upon a template]()

  [Document Manipulation Component]()

  #### Versioning

  ##### What do we want
  - Here, we would like to know what precisely was the state of a given document as of some particular instant in time.
  - As a business matter, the thing that has economic value and that is therefore referred to as "business component" for the purposes hereof is called a "version."
  - "Versioning" is a snapshot operation. "Versioning" and "version control" are not the same thing.

  ##### What is the problem
  - It is trivial to simply "save" a copy of a document somewhere.
  - It is also
    - costly: file I/O is computationally costly as a general matter. Here, it is doubly so because the documents are large.
    - cumbersome: need to either remember where you saved the copy or else provide a way to figure out where you saved the copy, or hard code a copy location for each version or some other such hacky maneuver
    - not exactly helpful: most problematically, when I ask for a prior version, I am asking for the difference between what I have now and what is in that version. If I ask for a prior version and you say "okay, here is your prior version", then I am required to proceed to step two, call up a redliner object, say "hey, compare this prior version to my current draft", and then have this redline-man give me yet another document that I then need to open and then review manually. Surely there must be a better way, especially since I am not merely "reviewing" to satisfy some general curiosity. There will always be a determination that I am trying ot make in respect of some change because, if there wasn't, then I would not have made the change in the first place. No one makes a change unless they believe that what they have changed to is better than the thing they had when they started. So, really, I am trying to figure out whether or not I am okay with some sort of change operation or, more specifically, the effect of such change operation. It would be nice if I could skip straight to this part. Whatever is the determination to be made, the making of a determination is an exercise in intelligence and an application of judgment--an exercise of my intelligence and an application of my judgment. Since this exercise of intelligence and this application of judgment will always result in the same answer being given to a question that is the same as some other question, our centeral interest here is in the mechanized discovery of these equalities. If I know that one question is the same as another, then, if I know what was the answer that was given in respect of such other question, I will, or should, necessarily know the answer presented to me now. 

  [Document Encryption Component]()

### Layout
  [Document Fragmentation Component](). Documents must be broken into fragments so that they may be processed on a single device. Fragmentation must consistent.

  [Document Layout Component]()

### Graphics
  [Document Graphics Component]()

  [Document Drawing Component]()

### Rendering
  [Document Animation Component]()

## Machine Learning

## Artificial Intelligence

