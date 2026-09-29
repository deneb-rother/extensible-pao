# Universal Letter-Based Major and Extensible PAO Systems

[![Release](https://img.shields.io/github/v/release/deneb-rother/ExtensiblePAO)](https://github.com/deneb-rother/ExtensiblePAO/releases)
![Release date](https://img.shields.io/github/release-date/deneb-rother/ExtensiblePAO)
![Last commit](https://img.shields.io/github/last-commit/deneb-rother/ExtensiblePAO)
![Repo size](https://img.shields.io/github/repo-size/deneb-rother/ExtensiblePAO)

[![Downloads](https://img.shields.io/github/downloads/deneb-rother/ExtensiblePAO/total)](https://github.com/deneb-rother/ExtensiblePAO/releases)
![Issues](https://img.shields.io/github/issues/deneb-rother/ExtensiblePAO)
![Contributors](https://img.shields.io/github/contributors/deneb-rother/ExtensiblePAO)
![Stars](https://img.shields.io/github/stars/deneb-rother/ExtensiblePAO)
![Forks](https://img.shields.io/github/forks/deneb-rother/ExtensiblePAO)

![Top language](https://img.shields.io/github/languages/top/deneb-rother/ExtensiblePAO)
![Languages](https://img.shields.io/github/languages/count/deneb-rother/ExtensiblePAO)

[![Code License](https://img.shields.io/badge/code-MIT-blue)](https://github.com/deneb-rother/ExtensiblePAO/LICENSE)
[![Content License](https://img.shields.io/badge/dataset-CC_BY--SA_4.0-green)](https://github.com/deneb-rother/ExtensiblePAO/LICENSE-CC)


## Background

When I tried to learn the PAO memorization technique, I quickly identified three problems:

- One of the most popular number-to-letter coding systems, the Major System, is based on pronunciation. This immediately creates two challenges. First, the way I pronounce a word affects its coding. As a non-native speaker, I may pronounce words correctly or incorrectly. More importantly, my pronunciation may change or improve over time, inevitably changing the coding of those words. From this perspective, such coding may not remain "fixed" over time. Moreover, if for any reason I wanted to switch to another language, I might get completely different coding for words that look the same or similar. For example, the letter "c" may be pronounced differently in English and Italian, as in the word "cinema". Working in multilingual environments may therefore be difficult because of this feature. For a "visual" person like me, it is also less natural to accept that the same letter, such as "c", can sometimes stand for 0 and sometimes for 7.

- An additional side effect of a phonetically anchored system is that the regular Major System ignores some letters or sounds, such as vowels or silent letters. Words or sounds such as "way" therefore cannot be coded using the system. While vowels and semivowels, by their nature, may not always be necessary to recognize a word, other sounds that may be silent in English but not in other languages can be crucial. Leaving them "out" of the system means that I cannot easily encode them into mnemonics.

- Another consideration is that I value flexibility. When I learn something, I do not like the method itself to limit me unless that limitation is an inherent feature of the method. The "standard" PAO system is based on two digits. It requires 100 images to be stored in memory in order to work with it. I am fine with that number, at least initially. But then I wondered: what if I wanted to have more? Or fewer? How could I effectively extend or reduce the existing system without forcing myself to relearn the entire set from scratch?

To address all of the above needs (plus a few others...), I tried to build a more straightforward system that is letter-based, easier to recall, and easier to extend. Of course, it does not offer full determinism, as that is impossible: we have only 10 digits and at least 26 letters in the most commonly used alphabets. It should not be considered also "superior" to anything that is known so far. I just think it may fit some specific needs better.

## Architecture

The architectural details of the systems are presented here:

- [Universal Letter-Based Major System](Universal_Letter-Based_Major_System.md)
- [Extensible PAO System](Extensible_PAO_System.md)

## Images

While LLM image generation is an extremely useful tool for building a decent PAO set, I am not sharing the ready-made PAO set in order to avoid potential licensing issues and the use of people's likenesses without permission. Instead, I provide the raw descriptions of the P-A-O characteristics, constructed according to the previously defined rules.

- [PAO Data (en}](data/PAO_data.en.csv)

To facilitate image generation, I am also sharing the prompt and the visual "grammar" that defines the rules for obtaining consistent output from an LLM:

- [PAO Scene Generation Prompt](PAO_Scene_Generation_Prompt.md)
- [PAO Visual Grammar](PAO_Visual_Grammar.md)


## PAO Card Generator

It is a template created in the Affinity format. It defines a master page and ties that with CSV data source. The data source needs to contain following fields:

```CSV
Code;Person;Object;Action;Instrument;Category;Picture
00;Arnold Schwarzenegger;dumbbell;lifting;;showbusiness;C:\Downloads\Project_PAO\pictures\00.png
```

The source file can be downloaded from here:
-[PAO Generator v.1.0](generators/PAO_generator_v.1.0.af)



## Other Supporting Materials

Additional supporting materials include:

- infographics for memorization and PAO set construction:
  - [Universal Language-Based Major System](infographics/en/ULMS_en.png)
  - [Extensible PAO](infographics/en/PAO_en.png)
- a manual explaining how to use the PAO system:
  - [PAO Manual](infographics/en/PAO_manual_en.pdf)
- the PAO source file in XLS format:
  - [PAO Data XLS](data/PAO_v.2.5.xls)

## Licensing

All PNG and PDF documents are shared under a CC-BY-SA 4.0 license.  
All other documents are shared under the MIT License.

