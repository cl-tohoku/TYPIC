# TYPIC: A Corpus of Template-Based Diagnostic Comments on Argumentation

## Overview
TYPIC is a corpus collected with the goal of providing specific diagnoses on an argumentation. It contains ten original arguments and 1,000 counterarguments, 197 of which are annotated with 1,082 diagnostic comments in both natural language and template formats. Diagnostic comments are annotated in Japanese and professionally translated into English.

![overview](https://github.com/cl-tohoku/TYPIC/blob/main/overview.jpg "overview")

## Dataset

### Original argument and Counterargument
The original arguments and counterarguments are stored in the files `original_arguments.json` and `counter_arguments.json` under the directory `arguments/{topic}`, respectively.
Each argument is represented as an object, the field `speech` contains the full text, and the field `sentences` includes an array of sentences.

###### Example of original argument
```
{
  "original_argument_id": "HW_PM_003",
  "speech": "Hello everyone. Today, we are given the motion that homework should be abolished. We defined that homework for primary students should be abolished. We have two points: First, some students tend to dislike studying. Secondly, we have more effective learning ways than homework. Let me explain our first argument. Some students tend to dislike studying but are obliged to do homework and most of students are not enthusiastic about homework. Studying, in fact, is not something to be obliged but rather for satisfying intellectual curiosity. Imagine one-year old babies. They are always looking around, crawling from corner to corner, and touching, even biting, everything unfamiliar to them. In this way, they learn new things and expand their understanding of the world. That’s how studying should be. It’s not good for students to be obliged to study by their teachers or parents. Being obliged will lead to problems between family. That’s one of the reasons some students tend to dislike studying. That is why homework should be abolished. Thank you.",
  "sentences": [
    "Hello everyone.",
    "Today, we are given the motion that homework should be abolished.",
    "......"
    "That is why homework should be abolished.",
    "Thank you."
  ]
},
```

###### Example of counterargument**
The field `original_argument_id` means the id of the original argument to be rebutted.
```
{
  "counter_argument_id": "HW_LO_205",
  "speech": "They said that being obliged will lead to problems between family. However, they might believe obliging homework can trigger family conflict, but it is not true, rather it is beneficial to generate some opportunity to communicate between the family. Let me imagine, if children have some questions about their homework, they will ask their parent and it will be good chance to deeply communicate. However, without homework from school, children have never study in home, so such kind of good opportunity does not occur in their paradigm. So we think their argument is not true.",
  "sentences": [
    "They said that being obliged will lead to problems between family.",
    "However, they might believe obliging homework can trigger family conflict, but it is not true, rather it is beneficial to generate some opportunity to communicate between the family.",
    "Let me imagine, if children have some questions about their homework, they will ask their parent and it will be good chance to deeply communicate.",
    "However, without homework from school, children have never study in home, so such kind of good opportunity does not occur in their paradigm.",
    "So we think their argument is not true."
  ],
  "original_argument_id": "HW_PM_003",
  "source": "PDA"
}
```

### Diagnostic comments 
The diagnostic comments are stored in files named `diagnostic_comments.json` under the `diagnoses/{lang}` directory.
Each diagnostic comment is represented as an object.

###### Description of some fields
| Field Name |Type| Description |
|:---|:---:|:---|
|counter_argument_id | `string` |The id of a counterargument to which a diagnostic comment is assigned. |
|target_sent_index | `array of number` |Index of an array of sentences to which diagnostic comment is assigned. The index starts from zero.|
|comment_in_natural_language | `string` |A diagnosis in natural language. |
|template_annotations | `array of object` |Annotation results for converting diagnostic comments in natural language to template format. In case of duplicate annotation by multiple annotators, each result is stored in an array. |
|template_id | `string` |The id of a selected template; see `diagnoses/{lang}/template_set.json` for the definition of the template. If none of the templates apply, it will be "OTHER." |
|template_text | `string` |Text of a template. If `template_id` is "OTHER," this field does not exist. |
|x, y, z | `string` |Placeholders in a template. If `template_id` is "OTHER," this field does not exist. |


###### Example of diagnostic comment
```
{
  "comment_id": "C01_HW_LO_205_6",
  "counter_argument_id": "HW_LO_205",
  "target_sent_index": [
      3
  ],
  "judge": "judgeA",
  "comment_in_natural_language": "Insufficient explanation of why homework is necessary as a topic of communication between parents and children, as other topics seem to exist as well.",
  "template_annotations": [
    {
      "annotation_id": "A01_HW_LO_205_6_1",
      "template": {
        "template_id": "CMP2",
        "template_text": "It lacks an explanation of why {x} is a better method to realize {y} instead of {z}",
        "x": "homework",
        "y": "family communication",
        "z": "other topics"
      },
      "annotator": "annotatorB"
    }
  ]
}
```


## Citation
If you use the data in your research, please cite the following paper.
```
@InProceedings{naito-EtAl:2022:LREC,
  author    = {Naito, Shoichi  and  Sawada, Shintaro  and  Nakagawa, Chihiro  and  Inoue, Naoya  and  Yamaguchi, Kenshi  and  Shimizu, Iori  and  Mim, Farjana Sultana  and  Singh, Keshav  and  Inui, Kentaro},
  title     = {TYPIC: A Corpus of Template-Based Diagnostic Comments on Argumentation},
  booktitle      = {Proceedings of the Language Resources and Evaluation Conference},
  year           = {2022},
  publisher      = {European Language Resources Association},
  pages     = {5916--5928},
  url       = {https://aclanthology.org/2022.lrec-1.636}
}
```

## License
TYPIC is distributed under the CC BY-SA 4.0 license. See  [LICENSE](https://github.com/cl-tohoku/TYPIC/blob/main/LICENSE)  for details.