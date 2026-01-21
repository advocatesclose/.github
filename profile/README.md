

# ADVOCATES CLOSE CORPORATION

Advocates Close (the "Company") is a company that develops technology for use by corporate attorneys. 

## Research and Experimentation

  - Business Component: A product that offers to clients the ability to prepare a registration statement and all documents required to be attached as exhibits thereto in respect of a SPAC IPO in 15 minutes or less.
  - This product has been in development for 48 months, 18 days and 4 hours as of this writing.
  - Development has required the creation of numerous other business components.

## Business Components

The following business components have been developed.

### Document Components

#### I/O Components

  [Document Reading Component]()

  [Document Formatting Component]()
  
  [Document Comparison Component]()
  
  [Document Persistence Component]()
  
  [Document Printing Component]()

#### Content Components

##### Templating Components

  [Creating a template]()

  [Reading from a template]()

  [Writing to a template]()

  [Operating upon a template]()

  [Document Manipulation Component]()

  [Document Versioning Component]()

### Versioning Components
  
  ###### What do we want
  - Here, we would like to know what precisely was the state of a given document as of some particular instant in time.
  - As a business matter, the thing that has economic value and that is therefore referred to as "business component" for the purposes hereof is called a "version."
  - "Versioning" is a snapshot operation. "Versioning" and "version control" are not the same thing.

  ##### What is the problem
  - It is trivial to simply "save" a copy of a document somewhere.
  - It is also
    - costly: file I/O is computationally costly as a general matter. Here, it is doubly so because the documents are large.
    - cumbersome: need to either remember where you saved the copy or else provide a way to figure out where you saved the copy, or hard code a copy location for each version or some other such hacky maneuver
    - not exactly helpful: most problematically, when I ask for a prior version, I am asking for the difference between what I have now and what is in that version. If I ask for a prior version and you say "okay, here is your prior version", then I am required to proceed to step two, call up a redliner object, say "hey, compare this prior version to my current draft", and then have this redline-man give me yet another document that I then need to open and then review manually. Surely there must be a better way, especially since I am not merely "reviewing" to satisfy some general curiosity. There will always be a determination that I am trying ot make in respect of some change because, if there wasn't, then I would not have made the change in the first place. No one makes a change unless they believe that what they have changed to is better than the thing they had when they started. So, really, I am trying to figure out whether or not I am okay with some sort of change operation or, more specifically, the effect of such change operation. It would be nice if I could skip straight to this part. Whatever is the determination to be made, the making of a determination is an exercise in intelligence and an application of judgment--an exercise of my intelligence and an application of my judgment. The fact that the related intelligence to be exercised and the judgmnent to be applied is mine is important because stationarity. 
    - The problem is thus that, as things stand, I am required to identify a difference, assess its effect on things that I care about, determine my "okayness" with each such effect and then communicate the determination that I have made and the finality thereof. Since the effect of a change is determined in respect of the set that is defined by "things that I care about" and since the elements of that set will change on a case-by-case basis, the problem is to systematize the manner in which changes are projected onto this set.
    - I have a set of changes and I have a set of things that I care about. The question is to map each element in the set of changes to zero or more elements in the set of things that I care about.
    - I will then need to map from that mapping into a space of utilities.

  ##### What is the information of a technological nature that we would like to discover?

  ##### What is genuinely uncertain in regards to such information?
  Projectioning. 
  
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

## Security
  [Document Encryption Component]()
