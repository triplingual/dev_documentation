---
description: Parsing of wikipedia made easy
---

# wikipedia\_for\_humans

{% embed url="https://github.com/HelloChatterbox/wikipedia\_for\_humans" %}

## Install

```bash
pip install wikipedia_for_humans
```

## Usage

For humans / voice assistants / chatbots

```python
import wikipedia_for_humans

# ask - search paragraphs
answer = wikipedia_for_humans.summary("dog")

"""
The dog (Canis familiaris when considered a distinct species or 
Canis lupus familiaris when considered a subspecies of the wolf) is a 
member of the genus Canis (canines), which forms part of the wolf-like canids, 
and is the most widely abundant terrestrial carnivore. The dog and the 
extant (...) """

answer = wikipedia_for_humans.ask_about("lifespan", "dog")

"""
In 2013, a study found that mixed breeds live on average 1.2 years longer 
than pure breeds, and that increasing body-weight was negatively correlated 
with longevity .The typical lifespan of dogs varies widely among breeds, but 
for most the median longevity, the age at which half the dogs in a population
 have died and half are still alive, ranges from 10 to 13 years. Individual
  dogs may live well beyond the median of their breed.
"""


answer = wikipedia_for_humans.ask_about("wolf", "dog")
"""
'Although dogs are the most abundant and widely distributed terrestrial '
 'carnivores, the potential of feral and free-ranging dogs to compete with '
 'other large carnivores is limited by their strong association with humans. '
 'For example, a review of the studies in the competitive effects of dogs on '
 'sympatric carnivores did not mention any research on competition between '
 'dogs and wolves. Although wolves are known to kill dogs, they tend to live '
 'in pairs or in small packs in areas where they are highly persecuted, giving '
 'them a disadvantage facing large dog groups.Wolves kill dogs wherever they '
 'are found together. One study reported that in Wisconsin in 1999 more '
 'compensation had been paid for losses due to wolves taking dogs than for '
 'wolves taking livestock. In Wisconsin wolves will often kill hunting dogs, '
 "possibly because the dogs are in the wolf's territory. (...)
 """

# tldr - search sentences
answer = wikipedia_for_humans.tldr("dog")
"""
The dog  is a member of the genus Canis , which forms part of the wolf-like canids, and is the most widely abundant terrestrial carnivore
"""

answer = wikipedia_for_humans.tldr_about("lifespan", "dog")
"""
the heavier the dog the shorter its lifespan
"""

answer = wikipedia_for_humans.tldr_about("wolf", "dog")
"""
The dog and the extant gray wolf are sister taxa, as modern wolves are not closely related to the population of wolves that was first domesticated
"""
```

parsing content

```python
import wikipedia_for_humans

# searching pages
pages = wikipedia_for_humans.search_pages("dogs", 5)

for page_name in pages:
    page = wikipedia_for_humans.get_page(page_name)
    print(page["title"], ":", page["summary"][:60])

# search in page content
search_term = "wolf"
page_name = "dog"
best_paragraph, score = wikipedia_for_humans.search_in_page(search_term,
                                                            page_name)
best_sentence, score = wikipedia_for_humans.search_in_page(search_term,
                                                           page_name,
                                                           paragraphs=False)

print("### Sentence level scores for", search_term)
for sentence, score in wikipedia_for_humans.search_sentences(search_term,
                                                             page_name):
    print(score, sentence)

"""
### Sentence level scores for wolf
0.9805825242718447 The dog and the extant gray wolf are sister taxa, as modern wolves are not closely related to the population of wolves that was first domesticated
0.9152542372881356 A strategy has been reported in Russia where one wolf lures a dog into heavy brush where another wolf waits in ambush
0.6920415224913494 Although the numbers of dogs killed each year are relatively low, it induces a fear of wolves entering villages and farmyards to take dogs, and losses of dogs to wolves has led to demands for more liberal wolf hunting regulations
0.6299212598425197 The temporalis muscle that closes the jaws is more robust in wolves
0.5989304812834225 The paws of a dog are half the size of those of a wolf, and their tails tend to curl upwards, another trait not found in wolves
0.5925925925925926 The teeth of gray wolves are also proportionately larger than those of dogs
0.5825242718446602 One study reported that in Wisconsin in 1999 more compensation had been paid for losses due to wolves taking dogs than for wolves taking livestock
0.5521472392638037 In Wisconsin wolves will often kill hunting dogs, possibly because the dogs are in the wolf's territory
0.5504587155963303 Wolves kill dogs wherever they are found together
0.5405405405405406 Dogs generally have brown eyes and wolves almost always have amber or light colored eyes
0.49079754601227 Wolves do not have dewclaws on their back legs, unless there has been admixture with dogs that had them
0.4823529411764706 He classified the domestic dog as Canis familiaris, and on the next page he classified the wolf as Canis lupus
0.46875 Dogs generally show reduced fear and aggression compared with wolves
0.4395604395604396 Domesticated dogs are clearly distinguishable from wolves by starch gel electrophoresis of red blood cell acid phosphatase
0.4347826086956522 Most dogs lack a functioning pre-caudal gland and enter estrus twice yearly, unlike gray wolves which only do so once a year
0.418848167539267 This has been made more complicated by the recent proposal that an initial wolf population split into East and West Eurasian groups
0.4166666666666667 The domestication of animals commenced over 15,000 years ago, beginning with the grey wolf (Canis lupus) by nomadic hunter-gatherers
0.37962962962962965 Linnaeus considered the dog to be a separate species from the wolf because of its cauda recurvata - its upturning tail which is not found in any other canid
0.37037037037037035 Domestic dogs inherited complex behaviors, such as bite inhibition, from their wolf ancestors, which would have been pack hunters with complex body language
0.3658536585365853 In 2016, a study found that there were only 11 fixed genes that showed variation between wolves and dogs
0.3571428571428572 Despite their close genetic relationship and the ability to inter-breed, there are a number of diagnostic features to distinguish the gray wolves from domestic dogs
0.30888030888030893 Christopher Wozencraft listed under the wolf Canis lupus its wild subspecies, and proposed two additional subspecies: "familiaris Linneaus, 1758 [domestic dog]" and "dingo Meyer, 1793 [domestic dog]"
0.30769230769230765 The genetic divergence between dogs and wolves occurred between 40,000–20,000 years ago, just before or during the Last Glacial Maximum
0.29007633587786263 The relationship between the presence of a dog and success in the hunt is often mentioned as a primary reason for the domestication of the wolf, and a 2004 study of hunter groups with and without a dog gives quantitative support to the hypothesis that the benefits of cooperative hunting was an important factor in wolf domestication
0.27702702702702703 In 2020, a literature review of canid domestication stated that modern dogs were not descended from the same Canis lineage as modern wolves, and proposes that dogs may be descended from a Pleistocene wolf closer in size to a village dog
0.26905829596412556 For example, a review of the studies in the competitive effects of dogs on sympatric carnivores did not mention any research on competition between dogs and wolves
0.2608695652173913 In 1999, a study of mitochondrial DNA indicated that the domestic dog may have originated from multiple grey wolf populations, with the dingo and New Guinea singing dog "breeds" having developed at a time when human populations were more isolated from each other
0.2605042016806723 Although wolves are known to kill dogs, they tend to live in pairs or in small packs in areas where they are highly persecuted, giving them a disadvantage facing large dog groups
0.25641025641025644 In some instances, wolves have displayed an uncharacteristic fearlessness of humans and buildings when attacking dogs, to the extent that they have to be beaten off or killed
0.2247191011235955 Another study indicated that after undergoing training to solve a simple manipulation task, dogs that are faced with an insoluble version of the same problem look at the human, while socialized wolves do not"""

print("### Paragraph level scores for", search_term)
for paragraph, score in wikipedia_for_humans.search_paragraphs(search_term,
                                                               page_name):
    print(score, paragraph)

"""
### Paragraph level scores for wolf
0.2725190839694656
 'Although dogs are the most abundant and widely distributed terrestrial '
 'carnivores, the potential of feral and free-ranging dogs to compete with '
 'other large carnivores is limited by their strong association with humans. '
 'For example, a review of the studies in the competitive effects of dogs on '
 'sympatric carnivores did not mention any research on competition between '
 'dogs and wolves. Although wolves are known to kill dogs, they tend to live '
 'in pairs or in small packs in areas where they are highly persecuted, giving '
 'them a disadvantage facing large dog groups.Wolves kill dogs wherever they '
 'are found together. (...)

0.19205298013245026
 "The origin of the domestic dog includes the dog's evolutionary divergence "
 'from the wolf, its domestication, and its development into dog types and dog '
 'breeds. The dog is a member of the genus Canis, which forms part of the '
 'wolf-like canids, and was the first species and the only large carnivore to '
 'have been domesticated. The dog and the extant gray wolf are sister taxa, as '
 'modern wolves are not closely related to the population of wolves that was '
 'first domesticated.The genetic divergence between dogs and wolves occurred '
 'between 40,000–20,000 years ago, (...)
"""
```

page disambiguation

```python
import wikipedia_for_humans

page = "Mercury"

# automatic disambiguation in all "human" methods should pick most common usage
answer = wikipedia_for_humans.tldr(page)
answer = wikipedia_for_humans.tldr_about("health", page)


# manually handle disambiguation pages
# NOTE: new_search_term is not guaranteed to be a valid page name
new_search_term, score = wikipedia_for_humans.disambiguate(page)
print(new_search_term, ":", wikipedia_for_humans.tldr(new_search_term))
"""
Mercury (element) : Mercury is a chemical element with the symbol Hg and atomic number 80 
"""

new_search_term, score = wikipedia_for_humans.disambiguate(page, "planet")
print(new_search_term, ":", wikipedia_for_humans.tldr(new_search_term))
"""
Mercury (planet) : Mercury is the smallest and innermost planet in the Solar System 
"""

new_search_term, score = wikipedia_for_humans.disambiguate(page, "god")
print(new_search_term, ":", wikipedia_for_humans.tldr(new_search_term))
"""
Mercury (mythology) : Mercury is a major god in Roman religion and mythology, being one of the 12 Dii Consentes within the ancient Roman pantheon 
"""

print("######## Top Candidate Pages")
# inspect disambiguation results
for candidate, score in wikipedia_for_humans.disambiguate(page, all_matches=True):
    print(score, candidate)

"""
0.5 Mercury (element), a metallic chemical element with the symbol 'Hg'
0.5 Mercury (mythology), a Roman god
0.5 Mercury (planet), the nearest to the Sun
"""


print("######## All Candidate Pages matching {films}")
for candidate, score in wikipedia_for_humans.disambiguate(page, "films", all_matches=True):
    if score >= 0.4:
        print(score, candidate)

"""
1.0 Mercury (film)
0.8 A fictional Minnesota town in the 2011 film Young Adult
0.4 The Mercury Cinema
"""
```

