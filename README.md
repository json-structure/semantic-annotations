<!-- regenerate: off (set to off if you edit this file) -->

# JSON Structure: Semantic and Reference-System Annotations

This is the working area for the individual Internet-Draft, "JSON Structure:
Semantic and Reference-System Annotations".

* [Editor's Copy](https://json-structure.github.io/semantic-annotations/#go.draft-vasters-json-structure-semantic-annotations.html)
* [Datatracker Page](https://datatracker.ietf.org/doc/draft-vasters-json-structure-semantic-annotations)
* [Individual Draft](https://datatracker.ietf.org/doc/html/draft-vasters-json-structure-semantic-annotations)
* [Compare Editor's Copy to Individual Draft](https://json-structure.github.io/semantic-annotations/#go.draft-vasters-json-structure-semantic-annotations.diff)


## Contributing

See the
[guidelines for contributions](https://github.com/json-structure/units/blob/main/CONTRIBUTING.md).

Contributions can be made by creating pull requests.
The GitHub interface supports creating pull requests using the Edit (✏) button.


## Scope and Non-goals

A quality of a value earns a keyword here when a consumer must know it to decide
whether two values may be combined or compared, and when it holds for the type
rather than varying from one instance to the next.

Scope:

* Defines optional annotations for observation-oriented semantics in JSON
	Structure schemas: `concepts`, `semanticRole`, `observedProperty`,
	`phenomenonTimeRelation`, `derivation`, `statistic`,
	`temporalReferenceSystem`, `cadence`, `coordinateReferenceSystem`,
	`vectorReferenceFrames`, `tensorReferenceFrames`, `frameTransforms`,
	`linearReferenceSystem`, `referenceRole`, `colorSpaces`, `audioChannels`,
	`spectralBands`, `codedValues`, and `measurementConditioning`.
* Covers roles for observation results, time semantics, quality,
	feature-of-interest variants, and observing procedure.
* Defines bindings for temporal, coordinate, vector-frame, tensor-frame, and
	linear reference systems, and for transformations between frames.
* Defines bindings for color spaces, audio channel layouts, spectral bands, and
	external code lists.
* Defines derivation, cadence, and measurement-conditioning annotations for
	result interpretation.

Non-goals:

* It is not a full ISO 19156 model or a normative JSON encoding of that model.
	It defines a role vocabulary laid over a record someone else designed, not an
	observation as a type to instantiate, classes for procedures or features, or
	relationships among observation entities. No record has to be shaped like an
	observation to carry these annotations.
* It does not define complete vocabularies for observed properties,
	procedures, quality values, or features of interest.
* It does not define identity or general relationship semantics
	(see JSON Structure Relations).
* It does not define units or conversion behavior
	(see JSON Structure Units).
* It does not define analytical procedures. It names summary functions but does
	not define what they compute, how gaps are treated, whether a window is
	inclusive, or whether a consumer may recompute a value.
* It does not define causal interpretation,
	execution policy, governance policy, or lineage policy.

Reference alignment:

* Observation concepts align with ISO 19156 and OGC Topic 20.
* Temporal terminology draws on ISO 19108, OGC Topic 25, ISO 19111 temporal
	CRS provisions, and GML 3.2.1 temporal schemas.


## Samples

Forty-three worked examples live in
[`samples/semantic-annotations/`](https://github.com/json-structure/primer-and-samples/tree/main/samples/semantic-annotations)
in the [primer-and-samples](https://github.com/json-structure/primer-and-samples)
repository. Each directory contains a `schema.struct.json` that declares the
extension meta-schema
[`semantic-annotations-v0.json`](semantic-annotations-v0.json) and an
`example.json` instance that conforms to it.

Fifteen teaching samples introduce the annotations one theme at a time, and
twenty-eight real-world samples annotate schemas published by live open-data
feeds and standing reference datasets, one per domain and publisher. Both sets
are catalogued in the
[samples README](https://github.com/json-structure/primer-and-samples/blob/main/samples/semantic-annotations/README.md)
and the
[real-world README](https://github.com/json-structure/primer-and-samples/blob/main/samples/semantic-annotations/real-world/README.md).

Where a sample carries an `enum`, the meaning of each symbol is stated with
`altenums` from the
[Alternate Names](https://json-structure.github.io/alternate-names/) extension —
a `lang:en` display label and a `description` sentence per symbol — rather than
packed into the description of the enclosing member.

Six of the real-world samples also carry a `schema-unannotated.struct.json`
holding the same record with the semantic layer removed, so that the two can be
read side by side. See
[what the annotations carry](https://github.com/json-structure/primer-and-samples/blob/main/samples/semantic-annotations/real-world/README.md#what-the-annotations-carry).

The tooling stays here. Run
[`samples/validate-samples.ps1`](samples/validate-samples.ps1) to check every
schema, every instance, and every annotation; it expects
`json-structure/primer-and-samples` to be checked out beside this repository.

## Schema comprehension evaluation

Every sample was put in front of an isolated language model (`GPT-5 mini`). Each
run received only two files — the sample's `schema.struct.json` and its
`example.json`, copied into a neutral sandbox with no repository, directory
names, or specification text — and was asked to propose the valuable analytics
dimensions the stream supports and why, then to flag any ambiguities and rate
its own confidence.

**Read the result as an observation, not as evidence.** The method has four
defects, and they are not incidental: the score is the subject's opinion of
itself, 40 of the 43 samples were run without an unannotated control, nothing
was blinded, and one model is one data point. What the run supports is that the
annotations are discoverable from the schema and get used. It does not support a
claim about how much difference they make, because for most samples nothing was
run without them.

What is worth reporting from it is not the confidence ratings but which
annotations the transcripts turned on, which is checkable:

* Agents used `temporalReferenceSystem` meta-types to *refuse* a mapping to UTC
	that the schema does not license, `coordinateReferenceSystem` to require
	axis-order and vertical-datum handling rather than assuming lat/lon,
	`vectorReferenceFrames`/`tensorReferenceFrames` to mark spacecraft-local
	components as not cross-comparable while treating the frame-invariant
	magnitude as comparable, `measurementConditioning` to recover A-weighting and
	the reference sound pressure, `codedValues` to plan registry joins against
	published code lists, and `spectralBands` to construct band-difference
	features.
* One transcript did the opposite and is more instructive: it reconstructed
	audio frame timing by dividing a frame counter by a member called
	`sample_rate`, a relation nothing in the schema stated. That is the failure
	mode the document is about, it went unremarked in the first write-up, and
	fixing it changed the specification and the sample rather than the
	evaluation.

Method, per-sample results, and the full list of caveats are in
[`EVALUATION.md`](EVALUATION.md). A controlled version — mechanically derived
rubric, an unannotated control arm for every sample, blinded grading by a
separate supervisor model, and a reported rate of positively wrong statements
per arm — is in [`evaluation/`](evaluation/), together with an account of what
it still cannot establish.


## Command Line Usage

Formatted text and HTML versions of the draft can be built using `make`.

```sh
$ make
```

Command line usage requires that you have the necessary software installed.  See
[the instructions](https://github.com/martinthomson/i-d-template/blob/main/doc/SETUP.md).
