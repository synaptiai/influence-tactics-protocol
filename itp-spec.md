# Influence Tactics Protocol (ITP) Specification
## v1.1

### Abstract

This document specifies the Influence Tactics Protocol (ITP), an open standard for detecting, scoring, and communicating information manipulation in digital content. The protocol enables interoperable manipulation detection across platforms while preserving user autonomy and preventing censorship.

The ITP defines a comprehensive 20-category assessment framework organized into five composite factors, producing a final 0-100 manipulation score.

### Terminology and Conventions

The key words "MUST", "MUST NOT", "REQUIRED", "SHALL", "SHALL NOT", "SHOULD", "SHOULD NOT", "RECOMMENDED", "MAY", and "OPTIONAL" in this document are to be interpreted as described in [RFC 2119].

### 1. Introduction

#### 1.1 Purpose
The ITP provides a standardized method for:
- Analyzing content for manipulation techniques
- Generating reproducible manipulation scores
- Sharing scores across platforms and applications
- Building consensus through distributed validation
- Educating users about manipulation patterns

#### 1.2 Design Principles
1. **Transparency**: All scoring methods must be explainable
2. **Interoperability**: Any system can implement the protocol
3. **Privacy**: No mandatory user tracking or identification
4. **Education**: Focus on teaching patterns, not declaring truth
5. **Decentralization**: No single point of control or failure

#### 1.3 Terminology
- **ITP Score**: Numerical assessment of manipulation likelihood (0-100)
- **Category**: Individual manipulation technique being measured (1-5 scale)
- **Composite Factor**: Aggregation of related categories into five primary dimensions
- **Validator**: Entity (human or AI) that scores content
- **Consensus**: Aggregated agreement across validators
- **Perspective**: Alternative interpretation of content intent

#### 1.4 Scoring System Architecture

The ITP employs a hierarchical scoring system:

**Level 1: 20 Individual Categories** (1-5 scale each)
- Each category measures a specific manipulation technique
- Scored based on objective, measurable criteria
- Provides granular, explainable assessments

**Level 2: 5 Composite Factors** (weighted averages of categories)
- Groups related categories into broader manipulation dimensions
- Provides high-level summary for users
- Maintains traceability to underlying categories

**Level 3: Overall Score** (0-100 scale)
- Weighted combination of all composite factors
- Provides single manipulation risk assessment
- Scaled for intuitive interpretation

#### 1.5 Category-to-Composite Factor Mapping

| # | Category | Question | Composite Factor | Weight |
|---|----------|----------|-----------------|--------|
| **EMOTIONAL MANIPULATION** | | | |
| 1 | Emotional Manipulation | Does it provoke fear, outrage, or guilt without solid evidence? | Emotional Manipulation | 0.35 |
| 2 | Call for Urgent Action | Does it demand immediate decisions without reflection? | Emotional Manipulation | 0.20 |
| 3 | Overuse of Novelty | Is the event framed as shocking or unprecedented? | Emotional Manipulation | 0.15 |
| 4 | Emotional Repetition | Are the same emotional triggers repeated excessively? | Emotional Manipulation | 0.15 |
| 5 | Manufactured Outrage | Does outrage seem sudden or disconnected from facts? | Emotional Manipulation | 0.15 |
| **SUSPICIOUS TIMING** | | | |
| 6 | Timing | Does the timing feel suspicious or coincidental with other events? | Suspicious Timing | 0.50 |
| 7 | Financial/Political Gain | Do powerful groups benefit disproportionately? | Suspicious Timing | 0.35 |
| 8 | Historical Parallels | Does the story mirror manipulative past events? | Suspicious Timing | 0.15 |
| **UNIFORM MESSAGING** | | | |
| 9 | Uniform Messaging | Are key phrases or ideas repeated across media? | Uniform Messaging | 0.50 |
| 10 | Bandwagon Effect | Is there pressure to conform because "everyone is doing it"? | Uniform Messaging | 0.25 |
| 11 | Rapid Behavior Shifts | Are groups adopting symbols or actions without clear reasoning? | Uniform Messaging | 0.25 |
| **TRIBAL DIVISION** | | | |
| 12 | Tribal Division | Does it create an "us vs. them" dynamic? | Tribal Division | 0.40 |
| 13 | Simplistic Narratives | Is the story reduced to "good vs. evil" frameworks? | Tribal Division | 0.35 |
| 14 | False Dilemmas | Are only two extreme options presented? | Tribal Division | 0.25 |
| **MISSING INFORMATION** | | | |
| 15 | Missing Information | Are alternative views or critical details excluded? | Missing Information | 0.25 |
| 16 | Authority Overload | Are questionable "experts" driving the narrative? | Missing Information | 0.15 |
| 17 | Suppression of Dissent | Are critics silenced or labeled negatively? | Missing Information | 0.15 |
| 18 | Cherry-Picked Data | Are statistics presented selectively or out of context? | Missing Information | 0.20 |
| 19 | Logical Fallacies | Are flawed arguments used to dismiss critics? | Missing Information | 0.15 |
| 20 | Framing Techniques | Is the story shaped to control how you perceive it? | Missing Information | 0.10 |

**Composite Factor Weights** (for overall score calculation):
- Emotional Manipulation: 25%
- Suspicious Timing: 20%
- Uniform Messaging: 20%
- Tribal Division: 15%
- Missing Information: 20%

### 2. Core Data Structures

#### 2.1 Content Identifier
All content MUST be uniquely identified using SHA-256 hashing:

```json
{
  "content_hash": "sha256:e3b0c44298fc1c149afbf4c8996fb92427ae41e4649b934ca495991b7852b855",
  "content_type": "text/plain",
  "content_length": 1024,
  "platform": "twitter",
  "url": "https://twitter.com/user/status/123456789",
  "timestamp": "2024-01-15T10:30:00Z"
}
```

#### 2.2 ITP Score Structure
```json
{
  "version": "1.0",
  "content_hash": "sha256:...",
  "score": {
    "overall": 72.5,
    "confidence": 0.81,
    "composite_factors": {
      "emotional_manipulation": {
        "composite_value": 4.2,
        "confidence": 0.85,
        "categories": {
          "emotional_manipulation_base": {
            "value": 4,
            "weight": 0.35,
            "evidence": "High density of fear, outrage, and guilt triggers without solid evidence"
          },
          "call_for_urgent_action": {
            "value": 5,
            "weight": 0.20,
            "evidence": "Demands immediate decisions without reflection time"
          },
          "overuse_of_novelty": {
            "value": 4,
            "weight": 0.15,
            "evidence": "Event framed as shocking and unprecedented"
          },
          "emotional_repetition": {
            "value": 4,
            "weight": 0.15,
            "evidence": "Same emotional triggers repeated excessively"
          },
          "manufactured_outrage": {
            "value": 4,
            "weight": 0.15,
            "evidence": "Outrage seems sudden and disconnected from facts"
          }
        }
      },
      "suspicious_timing": {
        "composite_value": 3.8,
        "confidence": 0.72,
        "categories": {
          "timing": {
            "value": 4,
            "weight": 0.50,
            "evidence": "Published 2 hours before legislative vote"
          },
          "financial_political_gain": {
            "value": 4,
            "weight": 0.35,
            "evidence": "Cleanup company stands to gain lucrative government contracts"
          },
          "historical_parallels": {
            "value": 3,
            "weight": 0.15,
            "evidence": "Mirrors past events used for controversial legislation"
          }
        }
      },
      "uniform_messaging": {
        "composite_value": 4.5,
        "confidence": 0.91,
        "categories": {
          "uniform_messaging_base": {
            "value": 5,
            "weight": 0.50,
            "evidence": "Key phrases repeated identically across 12+ media outlets"
          },
          "bandwagon_effect": {
            "value": 4,
            "weight": 0.25,
            "evidence": "Pressure to conform because 'everyone is doing it'"
          },
          "rapid_behavior_shifts": {
            "value": 4,
            "weight": 0.25,
            "evidence": "Groups adopting symbols/actions without clear reasoning"
          }
        }
      },
      "tribal_division": {
        "composite_value": 3.1,
        "confidence": 0.68,
        "categories": {
          "tribal_division_base": {
            "value": 3,
            "weight": 0.40,
            "evidence": "Creates clear 'us vs. them' dynamic between locals and outsiders"
          },
          "simplistic_narratives": {
            "value": 4,
            "weight": 0.35,
            "evidence": "Story reduced to 'good vs. evil' framework, ignoring complexity"
          },
          "false_dilemmas": {
            "value": 3,
            "weight": 0.25,
            "evidence": "Only two extreme options presented"
          }
        }
      },
      "missing_information": {
        "composite_value": 3.9,
        "confidence": 0.79,
        "categories": {
          "missing_information_base": {
            "value": 4,
            "weight": 0.25,
            "evidence": "Alternative views and critical timeline details excluded"
          },
          "authority_overload": {
            "value": 4,
            "weight": 0.15,
            "evidence": "Questionable 'experts' with no environmental credentials drive narrative"
          },
          "suppression_of_dissent": {
            "value": 3,
            "weight": 0.15,
            "evidence": "Critics labeled 'deniers' without addressing their arguments"
          },
          "cherry_picked_data": {
            "value": 4,
            "weight": 0.20,
            "evidence": "Statistics presented selectively without methodology"
          },
          "logical_fallacies": {
            "value": 4,
            "weight": 0.15,
            "evidence": "Critics dismissed as 'out-of-touch elites' via ad hominem"
          },
          "framing_techniques": {
            "value": 4,
            "weight": 0.10,
            "evidence": "Story shaped to control perception, ignoring systemic factors"
          }
        }
      }
    },
    "risk_tier": "HIGH",
    "risk_emoji": "🟠",
    "risk_indicator": "!!"
  },
  "metadata": {
    "scorer": {
      "type": "ai",
      "identifier": "nci-model-v0.1",
      "version": "0.1.0"
    },
    "generated_at": "2024-01-15T10:30:15Z",
    "processing_time_ms": 342
  }
}
```

**Optional Risk Tier Fields**:

Implementations MAY include the following fields to provide human-readable risk classification:

| Field | Type | Description |
|-------|------|-------------|
| `risk_tier` | string | Risk classification: `LOW` (0-25), `MODERATE` (26-50), `HIGH` (51-75), `SEVERE` (76-100) |
| `risk_emoji` | string | Visual indicator emoji (e.g., 🟢, 🟡, 🟠, 🔴) |
| `risk_indicator` | string | Text indicator: `·` (low), `!` (moderate), `!!` (high), `!!!` (severe) |

These fields are OPTIONAL and MAY be omitted. When present, they MUST be consistent with the `overall` score.

#### 2.3 Perspective Structure
```json
{
  "content_hash": "sha256:...",
  "perspectives": {
    "manipulative_interpretation": {
      "summary": "This content appears designed to provoke immediate emotional response...",
      "key_points": [
        "Uses urgent language without substantiation",
        "Timing aligns with political event",
        "Omits contradicting information"
      ],
      "confidence": 0.76
    },
    "legitimate_interpretation": {
      "summary": "This content may reflect genuine concern about developing situation...",
      "key_points": [
        "Author has credible history on topic",
        "Some claims are verifiable",
        "Emotional tone matches severity of issue"
      ],
      "confidence": 0.61
    }
  },
  "generated_at": "2024-01-15T10:30:20Z"
}
```

#### 2.4 Validation Structure
```json
{
  "content_hash": "sha256:...",
  "validation": {
    "validator_id": "sha256:validator_hash",
    "validator_type": "human",
    "vote": {
      "agrees_with_score": true,
      "adjusted_score": 75,
      "confidence": 0.8
    },
    "feedback": {
      "missing_factors": ["cherry_picked_data"],
      "incorrect_factors": [],
      "additional_evidence": "Source has history of misleading claims"
    },
    "timestamp": "2024-01-15T10:35:00Z",
    "signature": "base64_encoded_signature"
  }
}
```

#### 2.5 Consensus Structure
```json
{
  "content_hash": "sha256:...",
  "consensus": {
    "ai_scores": {
      "count": 3,
      "average": 72.3,
      "variance": 2.1,
      "confidence": 0.82
    },
    "human_scores": {
      "count": 47,
      "average": 68.5,
      "variance": 8.3,
      "confidence": 0.71,
      "weighted_by_reputation": 69.8
    },
    "combined_score": {
      "value": 70.1,
      "confidence": 0.75,
      "agreement_level": "moderate"
    },
    "validations": 50,
    "last_updated": "2024-01-15T11:00:00Z"
  }
}
```

### 3. Scoring Methodology

#### 3.1 Scoring Scale
All individual categories use a 1-5 scale:
- **1**: Not present - No signs of manipulation
- **2**: Minimally present - Slight indicators
- **3**: Moderately present - Clear but not dominant
- **4**: Strongly present - Prominent indicators
- **5**: Overwhelmingly present - Clear, strong evidence of manipulation

#### 3.2 Category Definitions and Calculations

> **Note**: The **Calculation** sections within each category definition are **informative** (non-normative). They provide reference calculation methodologies that implementations MAY use. Implementations MAY use alternative calculation methods that produce scores within the defined 1-5 scale, provided they meet the scoring criteria for each level. See Appendix G for additional guidance on calculation methodology.

##### 3.2.1 Composite Factor: Emotional Manipulation
Techniques that exploit emotions to bypass rational analysis.

###### Category 1: Emotional Manipulation (Base)
**Question**: Does it provoke fear, outrage, or guilt without solid evidence?

**Calculation**:
```
EM_base = w1 * trigger_density + w2 * intensity_score + w3 * fear_anger_ratio

where:
- trigger_density = emotional_words / total_words
- intensity_score = average intensity of emotional words (1-5 scale)
- fear_anger_ratio = (fear_words + anger_words) / emotional_words
- w1, w2, w3 = weights (default: 0.4, 0.3, 0.3)

Scale mapping:
1: trigger_density < 0.02
2: trigger_density 0.02-0.05
3: trigger_density 0.05-0.10
4: trigger_density 0.10-0.15
5: trigger_density > 0.15
```

###### Category 2: Call for Urgent Action
**Question**: Does it demand immediate decisions without reflection?

**Calculation**:
```
urgency_score = w1 * urgency_word_density + w2 * deadline_pressure + w3 * time_constraint_severity

where:
- urgency_word_density = (now, immediately, urgent, critical words) / total_words
- deadline_pressure = presence of artificial time constraints (binary 0/1)
- time_constraint_severity = 1 / hours_given_for_action
- w1, w2, w3 = weights (default: 0.4, 0.3, 0.3)

Scale mapping:
1: No urgency language, reasonable timeline
2: Mild urgency, days to weeks given
3: Moderate urgency, 1-2 days given
4: Strong urgency, hours given
5: Extreme urgency, immediate action demanded
```

###### Category 3: Overuse of Novelty
**Question**: Is the event framed as shocking or unprecedented?

**Calculation**:
```
novelty_score = w1 * novelty_word_count + w2 * superlative_density + w3 * historical_comparison_absence

where:
- novelty_word_count = (unprecedented, shocking, never-before, first-time words) / total_words
- superlative_density = (most, biggest, worst, ever words) / total_words
- historical_comparison_absence = 1 - (historical_context_provided / expected_context)
- w1, w2, w3 = weights (default: 0.4, 0.3, 0.3)

Scale mapping:
1: Event contextualized historically
2: Some novelty language, proper context
3: Moderate novelty framing
4: Strong novelty emphasis, limited context
5: Overwhelming novelty claims, no historical context
```

###### Category 4: Emotional Repetition
**Question**: Are the same emotional triggers repeated excessively?

**Calculation**:
```
repetition_score = w1 * emotional_image_frequency + w2 * phrase_repetition_rate

where:
- emotional_image_frequency = count of repeated emotional imagery / total_length
- phrase_repetition_rate = repeated_emotional_phrases / unique_emotional_phrases
- w1, w2 = weights (default: 0.5, 0.5)

Scale mapping:
1: Varied emotional content
2: Some repetition (1-2 repeats)
3: Moderate repetition (3-5 repeats)
4: High repetition (6-10 repeats)
5: Excessive repetition (>10 repeats)
```

###### Category 5: Manufactured Outrage
**Question**: Does outrage seem sudden or disconnected from facts?

**Calculation**:
```
manufactured_outrage = w1 * outrage_velocity + w2 * fact_to_emotion_ratio

where:
- outrage_velocity = rate of outrage expression over time (social signals/hour)
- fact_to_emotion_ratio = emotional_expressions / factual_statements
- w1, w2 = weights (default: 0.5, 0.5)

Scale mapping:
1: Outrage proportional to facts
2: Slight emotion-fact imbalance
3: Moderate imbalance, rapid spread
4: Strong imbalance, viral spread
5: Extreme imbalance, coordinated viral spread
```

##### 3.2.2 Composite Factor: Suspicious Timing
Timing patterns and beneficiary analysis.

###### Category 6: Timing
**Question**: Does the timing feel suspicious or coincidental with other events?

**Calculation**:
```
timing_score = max(event_correlations) * recency_weight

where:
- event_correlations = correlation coefficient with known events
- recency_weight = 1 / (1 + hours_from_event/24)

Scale mapping:
1: No temporal correlation
2: Weak correlation (r < 0.3)
3: Moderate correlation (r 0.3-0.6)
4: Strong correlation (r 0.6-0.8)
5: Very strong correlation (r > 0.8)
```

###### Category 7: Financial/Political Gain
**Question**: Do powerful groups benefit disproportionately?

**Calculation**:
```
gain_score = w1 * beneficiary_power + w2 * benefit_magnitude + w3 * benefit_immediacy

where:
- beneficiary_power = scale of beneficiary influence (1-5)
- benefit_magnitude = economic/political value of benefit (1-5)
- benefit_immediacy = 1 / days_until_benefit_realized
- w1, w2, w3 = weights (default: 0.4, 0.4, 0.2)

Scale mapping based on composite:
1: No clear beneficiaries
2: Minor beneficiaries, small gains
3: Moderate beneficiaries, notable gains
4: Major beneficiaries, substantial gains
5: Massive beneficiaries, disproportionate gains
```

###### Category 8: Historical Parallels
**Question**: Does the story mirror manipulative past events?

**Calculation**:
```
parallel_score = similarity_to_known_psyops

Scoring criteria:
1: No parallels to known manipulation campaigns
2: Weak similarities, likely coincidental
3: Moderate similarities in 1-2 dimensions
4: Strong similarities across 3-4 dimensions
5: Near-identical pattern to documented PSYOP
```

##### 3.2.3 Composite Factor: Uniform Messaging
Indicators of coordinated messaging.

###### Category 9: Uniform Messaging (Base)
**Question**: Are key phrases or ideas repeated across media?

**Calculation**:
```
uniform_messaging = (identical_phrases / total_phrases) * source_diversity_penalty

where:
- identical_phrases = phrases appearing in 3+ sources
- total_phrases = unique key phrases in content
- source_diversity_penalty = 1 - (unique_sources / total_sources)

Scale mapping:
1: High diversity, unique framing
2: Low uniformity (10-20% phrase overlap)
3: Moderate uniformity (20-40% overlap)
4: High uniformity (40-60% overlap)
5: Extreme uniformity (>60% overlap)
```

###### Category 10: Bandwagon Effect
**Question**: Is there pressure to conform because "everyone is doing it"?

**Calculation**:
```
bandwagon_score = w1 * conformity_pressure + w2 * popularity_claims + w3 * social_proof_frequency

where:
- conformity_pressure = count of "everyone agrees" type statements
- popularity_claims = references to majority opinion / total_claims
- social_proof_frequency = count of testimonials/endorsements
- w1, w2, w3 = weights (default: 0.4, 0.3, 0.3)

Scale mapping:
1: No conformity pressure
2: Mild social proof present
3: Moderate "everyone agrees" messaging
4: Strong bandwagon appeals
5: Overwhelming conformity pressure
```

###### Category 11: Rapid Behavior Shifts
**Question**: Are groups adopting symbols or actions without clear reasoning?

**Calculation**:
```
behavior_shift_score = adoption_velocity * coordination_indicator

where:
- adoption_velocity = new adopters per unit time
- coordination_indicator = temporal clustering coefficient

Scale mapping:
1: Organic, gradual adoption
2: Slightly accelerated adoption
3: Rapid adoption with some coordination
4: Very rapid, clearly coordinated adoption
5: Instantaneous, highly coordinated adoption
```

##### 3.2.4 Composite Factor: Tribal Division
Us-vs-them dynamics and polarization.

###### Category 12: Tribal Division (Base)
**Question**: Does it create an "us vs. them" dynamic?

**Calculation**:
```
tribal_division = w1 * pronoun_ratio + w2 * othering_language + w3 * group_identity_markers + w4 * dehumanization_score

where:
- pronoun_ratio = (we+us+our) / (they+them+their + 1)
- othering_language = count of exclusionary terms / total_words
- group_identity_markers = presence of in-group/out-group labels
- dehumanization_score = count of dehumanizing terms / total_words
  - Dehumanizing terms include: vermin, parasites, plague, infestation, animals,
    cockroaches, rats, disease, cancer, filth, scum, subhuman, and similar terms
    that strip humanity from the target group
  - This is the strongest indicator of tribal manipulation
- w1, w2, w3, w4 = weights (default: 0.25, 0.25, 0.25, 0.25)

Scale mapping:
1: Inclusive language, no division
2: Slight group differentiation
3: Moderate us-vs-them framing
4: Strong tribal messaging
5: Extreme polarization language (dehumanization present = automatic 5)
```

###### Category 13: Simplistic Narratives
**Question**: Is the story reduced to "good vs. evil" frameworks?

**Calculation**:
```
simplicity_score = w1 * complexity_absence + w2 * moral_absolutism

where:
- complexity_absence = 1 - (nuanced_statements / total_statements)
- moral_absolutism = (good/evil language count) / total_moral_statements
- w1, w2 = weights (default: 0.5, 0.5)

Scale mapping:
1: Highly nuanced, complex analysis
2: Some simplification, context maintained
3: Moderate simplification
4: Strong simplification, binary framing
5: Extreme reductionism, pure good vs. evil
```

###### Category 14: False Dilemmas
**Question**: Are only two extreme options presented?

**Calculation**:
```
false_dilemma_score = binary_choice_count / total_choices_presented

Scale mapping:
1: Multiple options presented (>3)
2: Few options but not strictly binary
3: Primarily binary, some alternatives mentioned
4: Strictly binary, alternatives dismissed
5: Absolute binary, "with us or against us"
```

##### 3.2.5 Composite Factor: Missing Information
Omissions, suppression, and incomplete presentation.

###### Category 15: Missing Information (Base)
**Question**: Are alternative views or critical details excluded?

**Calculation**:
```
missing_info = w1 * context_completeness + w2 * claim_substantiation + w3 * attribution_asymmetry

where:
- context_completeness = 1 - (provided_context / expected_context)
- claim_substantiation = unsubstantiated_claims / total_claims
- attribution_asymmetry = |credible_attributions - discrediting_attributions| / total_attributions
  - Credible attribution verbs: confirmed, revealed, proved, demonstrated, showed,
    established, documented, verified, found, discovered
  - Discrediting attribution verbs: claimed, alleged, insisted, asserted, maintained,
    contended, suggested, argued, speculated, pushed
  - High asymmetry indicates biased source treatment (favored vs. disfavored sources)
- w1, w2, w3 = weights (default: 0.35, 0.35, 0.30)

Attribution asymmetry scoring adjustment:
- Asymmetry > 0.7: Add +1 to base score
- Asymmetry > 0.5: Add +0.5 to base score

Scale mapping:
1: Comprehensive, all sides presented, balanced attribution
2: Minor omissions, mostly complete
3: Moderate omissions, key points missing
4: Major omissions, one-sided presentation, asymmetric attribution
5: Extreme omissions, critical info absent, strongly biased sourcing
```

###### Category 16: Authority Overload
**Question**: Are questionable "experts" driving the narrative?

**Calculation**:
```
authority_score = w1 * unqualified_expert_ratio + w2 * credentials_relevance + w3 * expert_diversity

where:
- unqualified_expert_ratio = experts without relevant credentials / total_experts
- credentials_relevance = 1 - (relevant_credentials / total_credentials)
- expert_diversity = 1 - (unique_expert_perspectives / total_expert_appearances)
- w1, w2, w3 = weights (default: 0.4, 0.3, 0.3)

Scale mapping:
1: Qualified, diverse expert pool
2: Mostly qualified, some questionable
3: Mixed credentials, limited diversity
4: Predominantly unqualified, uniform views
5: Exclusively unqualified "experts"
```

###### Category 17: Suppression of Dissent
**Question**: Are critics silenced or labeled negatively?

**Calculation**:
```
suppression_score = w1 * ad_hominem_attacks + w2 * dismissive_language + w3 * deplatforming_evidence

where:
- ad_hominem_attacks = personal attacks / total_responses_to_critics
- dismissive_language = dismissive terms (denier, conspiracy theorist) / total_critic_references
- deplatforming_evidence = documented cases of suppression (binary indicators)
- w1, w2, w3 = weights (default: 0.4, 0.3, 0.3)

Scale mapping:
1: Critics engaged substantively
2: Some dismissiveness, mostly substantive
3: Moderate ad hominem, some engagement
4: Predominantly ad hominem, little engagement
5: Complete suppression, labeling, deplatforming
```

###### Category 18: Cherry-Picked Data
**Question**: Are statistics presented selectively or out of context?

**Calculation**:
```
cherry_picking = w1 * data_selectivity + w2 * context_omission + w3 * methodology_transparency

where:
- data_selectivity = contradicting_data_ignored / total_relevant_data
- context_omission = 1 - (context_provided / required_context)
- methodology_transparency = 1 - (methodology_explained / methodology_required)
- w1, w2, w3 = weights (default: 0.4, 0.3, 0.3)

Scale mapping:
1: Comprehensive data, full context
2: Mostly complete, minor omissions
3: Moderate selectivity, some context
4: Highly selective, minimal context
5: Extreme cherry-picking, no context
```

###### Category 19: Logical Fallacies
**Question**: Are flawed arguments used to dismiss critics?

**Calculation**:
```
fallacy_score = Σ(fallacy_types * severity) / total_arguments

Common fallacies tracked:
- Ad hominem
- Straw man
- Appeal to authority
- False equivalence
- Slippery slope
- Red herring

Scale mapping:
1: No significant fallacies
2: 1-2 minor fallacies
3: 3-5 moderate fallacies
4: 6-10 significant fallacies
5: Pervasive fallacious reasoning
```

###### Category 20: Framing Techniques
**Question**: Is the story shaped to control how you perceive it?

**Calculation**:
```
framing_score = w1 * selective_emphasis + w2 * metaphor_use + w3 * perspective_limitation + w4 * pattern_detection

where:
- selective_emphasis = emphasized_points / total_relevant_points (bias measure)
- metaphor_use = manipulative_metaphors / total_metaphors
- perspective_limitation = 1 - (perspectives_presented / perspectives_available)
- pattern_detection = Σ(detected_patterns) / total_possible_patterns
  - Patterns to detect:
    1. Victim-villain-hero structure: Content assigns clear roles to create emotional narrative
    2. False balance: Equal weight given to unequal positions (e.g., expert vs. fringe view)
    3. Scope manipulation: Zooming in/out to distort significance (anecdote as trend, or trend as anecdote)
    4. Temporal framing: Presenting old issues as new crises, or current issues as ancient history
    5. Passive voice to obscure agency: "Mistakes were made" rather than "X made mistakes"
    6. Loaded language: Using charged terms that assume conclusions (e.g., "regime" vs. "government")
- w1, w2, w3, w4 = weights (default: 0.25, 0.25, 0.25, 0.25)

Scale mapping:
1: Neutral framing, multiple perspectives
2: Slight bias, mostly balanced
3: Moderate framing bias, 1-2 patterns detected
4: Strong framing, limited perspectives, 3-4 patterns detected
5: Extreme framing control, single perspective, 5+ patterns detected
```

#### 3.3 Composite Factor Calculation
Each composite factor is calculated as a weighted average of its component categories:

```
composite_factor = Σ(category_value * category_weight) / Σ(category_weights)

Default category weights by composite factor:

Emotional Manipulation:
- emotional_manipulation_base: 0.35
- call_for_urgent_action: 0.20
- overuse_of_novelty: 0.15
- emotional_repetition: 0.15
- manufactured_outrage: 0.15

Suspicious Timing:
- timing: 0.50
- financial_political_gain: 0.35
- historical_parallels: 0.15

Uniform Messaging:
- uniform_messaging_base: 0.50
- bandwagon_effect: 0.25
- rapid_behavior_shifts: 0.25

Tribal Division:
- tribal_division_base: 0.40
- simplistic_narratives: 0.35
- false_dilemmas: 0.25

Missing Information:
- missing_information_base: 0.25
- authority_overload: 0.15
- suppression_of_dissent: 0.15
- cherry_picked_data: 0.20
- logical_fallacies: 0.15
- framing_techniques: 0.10
```

#### 3.4 Overall Score Calculation
```
overall_score = Σ(composite_factor * composite_weight * factor_confidence)

where composite weights:
- emotional_manipulation: 0.25
- suspicious_timing: 0.20
- uniform_messaging: 0.20
- tribal_division: 0.15
- missing_information: 0.20

The sum of all weights equals 1.0

Score is then scaled to 0-100 range:
overall_score_100 = (overall_score - 1) * 25
```

#### 3.5 Confidence Calculation
```
confidence = min(
  data_completeness * model_certainty * validator_agreement,
  0.95  // Never claim 100% confidence
)

where:
- data_completeness = available_signals / required_signals
- model_certainty = model's internal confidence score
- validator_agreement = 1 - (std_dev(validator_scores) / 25)
```

### 4. API Specification

#### 4.1 Required Endpoints

##### 4.1.1 Analyze Content
```
POST /v1/analyze
Content-Type: application/json

Request:
{
  "content": "string (required)",
  "content_type": "text/plain|text/html|text/markdown",
  "semantic_content_type": "auto|news|social_media",
  "options": {
    "include_perspectives": true,
    "include_evidence": true,
    "language": "en"
  }
}

Response:
{
  "content_hash": "sha256:...",
  "score": { /* ITP Score Structure */ },
  "perspectives": { /* Perspective Structure */ },
  "status": "success"
}
```

**Request Fields**:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `content` | string | REQUIRED | Text content to analyze (50-1,000,000 characters) |
| `content_type` | string | OPTIONAL | MIME type: `text/plain` (default), `text/html`, `text/markdown` |
| `semantic_content_type` | string | OPTIONAL | Content category hint: `auto` (default), `news`, `social_media`. Enables context-aware analysis routing. |
| `options` | object | OPTIONAL | Analysis options (see below) |

**Options Object**:

| Field | Type | Default | Description |
|-------|------|---------|-------------|
| `include_perspectives` | boolean | `false` | Include red team/blue team analysis (Level 2+) |
| `include_evidence` | boolean | `true` | Include evidence for score justification (Level 3) |
| `language` | string | `"en"` | BCP 47 language tag for analysis |

##### 4.1.2 Get Score
```
GET /v1/score/{content_hash}

Response:
{
  "content_hash": "sha256:...",
  "score": { /* ITP Score Structure */ },
  "consensus": { /* Consensus Structure */ },
  "status": "success"
}
```

##### 4.1.3 Submit Validation
```
POST /v1/validate
Content-Type: application/json

Request:
{
  "content_hash": "sha256:...",
  "validation": { /* Validation Structure */ }
}

Response:
{
  "validation_id": "uuid",
  "status": "accepted"
}
```

##### 4.1.4 Get Consensus
```
GET /v1/consensus/{content_hash}

Response:
{
  "content_hash": "sha256:...",
  "consensus": {
    "consensus_score": 67.5,
    "ai_score": 72.3,
    "human_score": 65.8,
    "confidence": 0.78,
    "confidence_interval": {
      "lower": 62.1,
      "upper": 72.9
    },
    "validation_count": 47,
    "is_valid": true
  },
  "status": "success"
}
```

**Consensus Object Fields**:

| Field | Type | Required | Description |
|-------|------|----------|-------------|
| `consensus_score` | number | REQUIRED | Final weighted consensus score (0-100) |
| `ai_score` | number | REQUIRED | AI-generated score component |
| `human_score` | number | REQUIRED | Reputation-weighted average of human validator scores |
| `confidence` | number | REQUIRED | Overall confidence in the consensus (0.0-1.0) |
| `confidence_interval` | object | REQUIRED | Statistical confidence bounds with `lower` and `upper` fields |
| `validation_count` | integer | REQUIRED | Number of human validations included |
| `is_valid` | boolean | REQUIRED | Whether consensus meets minimum validity criteria |

The `is_valid` field MUST be `true` when `validation_count` meets the implementation's minimum threshold AND `confidence` exceeds the minimum confidence threshold.

#### 4.2 Optional Endpoints

##### 4.2.1 Batch Analysis
```
POST /v1/analyze/batch
Content-Type: application/json

Request:
{
  "items": [
    {"content": "...", "id": "..."},
    ...
  ]
}

Response:
{
  "results": [
    {"id": "...", "score": {...}},
    ...
  ]
}
```

##### 4.2.2 Historical Scores
```
GET /v1/history/{content_hash}

Response:
{
  "content_hash": "sha256:...",
  "history": [
    {"timestamp": "...", "score": {...}},
    ...
  ]
}
```

#### 4.3 Error Responses

All error responses MUST use the following structure:

```json
{
  "error": {
    "code": "ERROR_CODE",
    "message": "Human-readable description",
    "details": {}
  },
  "status": "error"
}
```

The `details` object MAY contain additional context specific to the error type.

##### 4.3.1 Error Codes

Implementations MUST support the following error codes:

| Code | HTTP Status | Description |
|------|-------------|-------------|
| `INVALID_REQUEST` | 400 | Malformed request body or parameters |
| `CONTENT_TOO_SHORT` | 400 | Content below minimum length (50 characters) |
| `CONTENT_TOO_LONG` | 400 | Content exceeds maximum length (1,000,000 characters default; implementations MAY specify different limits) |
| `INVALID_CONTENT_TYPE` | 400 | Unsupported `content_type` value |
| `INVALID_CONTENT_HASH` | 400 | Malformed SHA-256 hash format |
| `CONTENT_NOT_FOUND` | 404 | No score exists for the specified `content_hash` |
| `VALIDATION_NOT_FOUND` | 404 | Validation ID not found |
| `RATE_LIMIT_EXCEEDED` | 429 | Too many requests; see `Retry-After` header |
| `INTERNAL_ERROR` | 500 | Server error |

Implementations MAY define additional vendor-specific error codes using the format `vendor:error_code`.

##### 4.3.2 HTTP Status Codes

Implementations MUST return appropriate HTTP status codes:

| Status | Usage |
|--------|-------|
| 200 | Successful operation |
| 400 | Client error (invalid request, validation failure) |
| 404 | Resource not found |
| 429 | Rate limit exceeded |
| 500 | Server error |

Implementations SHOULD include the `Retry-After` header (in seconds) with 429 responses.

### 5. Display Requirements

#### 5.1 Nutritional Label Format

Implementations MUST display:
1. Overall score (0-100)
2. Confidence level
3. Primary manipulation factor (if score > 40)

Implementations SHOULD display:
1. All five factor scores
2. Red/blue perspectives
3. Consensus information
4. Evidence snippets

#### 5.2 Visual Representation

**Standard View (Composite Factors)**:
```
┌──────────────────────────────────────┐
│    Information Nutrition Label       │
├──────────────────────────────────────┤
│ Manipulation Score: 72 [!!]          │
│ Confidence: 81%                      │
├──────────────────────────────────────┤
│ COMPOSITE FACTORS                    │
│ Emotional Triggers    ████░ 4.2      │
│ Suspicious Timing     ███░░ 3.8      │
│ Uniform Messaging     ████░ 4.5      │
│ Tribal Division       ███░░ 3.1      │
│ Missing Context       ███░░ 3.9      │
├──────────────────────────────────────┤
│ Community: 68 (47 validators)        │
│ [See Detailed Scores] [Perspectives] │
└──────────────────────────────────────┘
```

**Detailed View (All 20 Categories)**:
```
┌──────────────────────────────────────┐
│    ITP Detailed Analysis             │
├──────────────────────────────────────┤
│ Manipulation Score: 72 [!!]          │
├──────────────────────────────────────┤
│ EMOTIONAL MANIPULATION (4.2)         │
│  • Base Emotional Triggers  ████░ 4  │
│  • Urgent Action Demands    █████ 5  │
│  • Overuse of Novelty       ████░ 4  │
│  • Emotional Repetition     ████░ 4  │
│  • Manufactured Outrage     ████░ 4  │
├──────────────────────────────────────┤
│ SUSPICIOUS TIMING (3.8)              │
│  • Timing Coincidence       ████░ 4  │
│  • Financial/Political Gain ████░ 4  │
│  • Historical Parallels     ███░░ 3  │
├──────────────────────────────────────┤
│ UNIFORM MESSAGING (4.5)              │
│  • Phrase Repetition        █████ 5  │
│  • Bandwagon Effect         ████░ 4  │
│  • Rapid Behavior Shifts    ████░ 4  │
├──────────────────────────────────────┤
│ TRIBAL DIVISION (3.1)                │
│  • Us vs. Them Dynamic      ███░░ 3  │
│  • Simplistic Narratives    ████░ 4  │
│  • False Dilemmas           ███░░ 3  │
├──────────────────────────────────────┤
│ MISSING INFORMATION (3.9)            │
│  • Context Omission         ████░ 4  │
│  • Authority Overload       ████░ 4  │
│  • Suppression of Dissent   ███░░ 3  │
│  • Cherry-Picked Data       ████░ 4  │
│  • Logical Fallacies        ████░ 4  │
│  • Framing Techniques       ████░ 4  │
├──────────────────────────────────────┤
│ [See Perspectives] [View History]    │
└──────────────────────────────────────┘
```

#### 5.3 Severity Indicators
- 0-25: Low manipulation risk [·]
- 26-50: Moderate manipulation risk [!]
- 51-75: High manipulation risk [!!]
- 76-100: Severe manipulation risk [!!!]

### 6. Validation & Consensus

#### 6.1 Validator Requirements

##### Human Validators
- Must complete training module
- Must maintain >60% accuracy on known examples
- Must provide reasoning for divergent scores

##### AI Validators
- Must publish model specifications
- Must achieve >70% accuracy on test set
- Must provide explainable outputs

#### 6.2 Reputation Calculation
```
reputation = base_reputation * accuracy_multiplier * consistency_multiplier * participation_multiplier

where:
- base_reputation = 0.5
- accuracy_multiplier = correct_validations / total_validations
- consistency_multiplier = 1 - variance(validator_scores)
- participation_multiplier = min(validations / 100, 1.0)
```

#### 6.3 Consensus Algorithm
```python
def calculate_consensus(validations):
    # Separate by validator type
    ai_scores = [v for v in validations if v.type == 'ai']
    human_scores = [v for v in validations if v.type == 'human']
    
    # Weight by reputation
    weighted_human = sum(v.score * v.reputation for v in human_scores) / sum(v.reputation for v in human_scores)
    
    # Combine with AI scores
    if ai_scores and human_scores:
        combined = 0.3 * mean(ai_scores) + 0.7 * weighted_human
    elif ai_scores:
        combined = mean(ai_scores)
    else:
        combined = weighted_human
    
    # Calculate confidence
    confidence = 1 - (std_dev(all_scores) / 50)  # Normalize variance
    
    return combined, confidence
```

### 7. Security Considerations

#### 7.1 Content Integrity
- All content MUST be hashed before analysis
- Hashes MUST use SHA-256 or stronger
- Original content SHOULD NOT be stored

#### 7.2 Validator Authentication
- Validators MUST sign their validations
- Signatures MUST use ED25519 or equivalent
- Public keys MUST be published

#### 7.3 Privacy Protection
- User identities MUST NOT be required
- IP addresses MUST NOT be logged
- Behavioral tracking MUST be optional

#### 7.4 Adversarial Resistance
- Score gaming detection via anomaly detection
- Sybil attack prevention via proof-of-work or stake
- Coordinated manipulation detection via timing analysis

#### 7.5 Transport Security

- API endpoints MUST be served over HTTPS
- Implementations MUST support TLS 1.2
- Implementations SHOULD support TLS 1.3
- Implementations MUST reject plaintext HTTP connections for API endpoints
- Implementations SHOULD use certificates signed by trusted Certificate Authorities
- Implementations SHOULD implement certificate pinning for high-security deployments

### 8. Implementation Guidelines

#### 8.0 Conformance Levels

Implementations declare conformance at one of three levels:

| Level | Name | Requirements |
|-------|------|--------------|
| 1 | ITP-Core | MUST calculate all 20 categories, 5 composite factors, and overall score. MUST provide JSON API with `/v1/analyze` endpoint. MUST return valid ITP Score Structure. |
| 2 | ITP-Validated | All Level 1 requirements, plus MUST support `/v1/validate` and `/v1/consensus` endpoints for distributed validation. |
| 3 | ITP-Full | All Level 2 requirements, plus MUST provide perspectives, detailed evidence, guidance, and all optional endpoints defined in §4.2. |

Implementations MUST declare their conformance level in API responses via the `X-ITP-Conformance-Level` header (value: `1`, `2`, or `3`).

Implementations MAY claim partial conformance by listing specific features implemented, but MUST NOT claim a conformance level without meeting all requirements for that level.

#### 8.1 Minimum Viable Implementation

> **Note**: This section details the requirements for **Level 1 (ITP-Core)** conformance. Implementations claiming Level 1 MUST satisfy all requirements below. See §8.0 for higher conformance levels.

To be considered protocol-compliant, implementations MUST:

1. **Support text content analysis**
   - Accept plain text, HTML, or markdown input
   - Handle content from 50 to at least 1,000,000 characters

2. **Calculate all 20 categories**
   - Implement scoring logic for each individual category
   - Use 1-5 scale for all category scores
   - Provide evidence/reasoning for each score

3. **Calculate 5 composite factors**
   - Aggregate category scores using specified weights
   - Maintain traceability to underlying categories
   - Calculate composite confidence scores

4. **Generate overall score**
   - Apply composite factor weights correctly
   - Scale final score to 0-100 range
   - Calculate overall confidence metric

5. **Provide JSON API**
   - Implement required endpoints (analyze, get_score)
   - Return complete data structures
   - Include all metadata

6. **Display nutrition label**
   - Show overall score and confidence
   - Display all 5 composite factors
   - Provide access to detailed category breakdown

**Note**: Implementations that calculate fewer than all 20 categories are NOT protocol-compliant and MUST NOT claim ITP compliance.

#### 8.2 Reference Implementation
Available at: https://github.com/synaptiai/influence-tactics-protocol

Languages:
- Python (scoring engine)
- JavaScript (browser extension)
- Go (API server)

#### 8.3 Testing Requirements

Implementations MUST:

1. **Pass protocol compliance test suite**
   - Correctly calculate all 20 category scores
   - Properly weight and aggregate into composite factors
   - Generate valid JSON structures
   - Handle all required API endpoints

2. **Achieve >70% accuracy on test corpus**
   - Tested against labeled historical examples
   - Category scores within ±1 point of ground truth
   - Overall scores within ±10 points of consensus

3. **Handle edge cases gracefully**
   - Empty or minimal content
   - Content in unsupported languages
   - Missing context information
   - Extreme or adversarial inputs

4. **Provide explainable outputs**
   - Every category score MUST have evidence
   - Weights MUST be documented
   - Calculations MUST be reproducible

5. **Performance requirements**
   - Single analysis: <5 seconds for 1000 words
   - Batch analysis: Scale linearly
   - API response time: <2 seconds p95

### 9. Extensibility

#### 9.1 Custom Factors
Implementations MAY add custom factors:
```json
{
  "factors": {
    "standard_factors": {...},
    "custom_factors": {
      "vendor:factor_name": {
        "value": 3.5,
        "confidence": 0.8
      }
    }
  }
}
```

#### 9.2 Language Support
Protocol supports extension to other languages:
- Language-specific factor weights
- Cultural context adjustments
- Multi-language training data

#### 9.3 Content Types
Future versions may support:
- Images (via OCR and visual analysis)
- Video (via transcript and visual analysis)
- Audio (via transcription)

### 10. Governance

#### 10.1 Protocol Evolution
- Changes require RFC process
- Major versions need 66% implementer agreement
- Backward compatibility for 2 major versions

#### 10.2 Training Data Governance
- Public corpus maintained by foundation
- Community contributions reviewed
- Quarterly updates to test sets

#### 10.3 Dispute Resolution
- Technical disputes: Technical committee
- Scoring disputes: Community consensus
- Governance disputes: Board vote

### 11. References

#### 11.1 Normative References

The following documents are referenced normatively in this specification:

- **[RFC 2119]** Bradner, S., "Key words for use in RFCs to Indicate Requirement Levels", BCP 14, RFC 2119, March 1997. https://datatracker.ietf.org/doc/html/rfc2119

- **[RFC 8259]** Bray, T., Ed., "The JavaScript Object Notation (JSON) Data Interchange Format", STD 90, RFC 8259, December 2017. https://datatracker.ietf.org/doc/html/rfc8259

- **[RFC 7231]** Fielding, R., Ed., and J. Reschke, Ed., "Hypertext Transfer Protocol (HTTP/1.1): Semantics and Content", RFC 7231, June 2014. https://datatracker.ietf.org/doc/html/rfc7231

- **[RFC 3339]** Klyne, G. and C. Newman, "Date and Time on the Internet: Timestamps", RFC 3339, July 2002. https://datatracker.ietf.org/doc/html/rfc3339

- **[JSON Schema]** Wright, A., et al., "JSON Schema: A Media Type for Describing JSON Documents", draft-bhutton-json-schema-01, December 2020. https://json-schema.org/draft/2020-12/json-schema-core.html

#### 11.2 Informative References

The following documents provide additional context but are not required for conformance:

- **[OWASP-API]** OWASP Foundation, "OWASP API Security Top 10". https://owasp.org/www-project-api-security/

- **[TLS 1.3]** Rescorla, E., "The Transport Layer Security (TLS) Protocol Version 1.3", RFC 8446, August 2018. https://datatracker.ietf.org/doc/html/rfc8446

### Appendix A: Example Implementation

```python
import hashlib
from typing import Dict, List, Tuple

class ITPImplementation:
    VERSION = "1.0"

    # Category weights within each composite factor
    WEIGHTS = {
        'emotional_manipulation': {
            'emotional_manipulation_base': 0.35,
            'call_for_urgent_action': 0.20,
            'overuse_of_novelty': 0.15,
            'emotional_repetition': 0.15,
            'manufactured_outrage': 0.15
        },
        'suspicious_timing': {
            'timing': 0.50,
            'financial_political_gain': 0.35,
            'historical_parallels': 0.15
        },
        'uniform_messaging': {
            'uniform_messaging_base': 0.50,
            'bandwagon_effect': 0.25,
            'rapid_behavior_shifts': 0.25
        },
        'tribal_division': {
            'tribal_division_base': 0.40,
            'simplistic_narratives': 0.35,
            'false_dilemmas': 0.25
        },
        'missing_information': {
            'missing_information_base': 0.25,
            'authority_overload': 0.15,
            'suppression_of_dissent': 0.15,
            'cherry_picked_data': 0.20,
            'logical_fallacies': 0.15,
            'framing_techniques': 0.10
        }
    }

    # Composite factor weights for overall score
    COMPOSITE_WEIGHTS = {
        'emotional_manipulation': 0.25,
        'suspicious_timing': 0.20,
        'uniform_messaging': 0.20,
        'tribal_division': 0.15,
        'missing_information': 0.20
    }

    def analyze(self, content: str, context: dict = None) -> dict:
        """
        Analyze content and generate ITP score.

        Args:
            content: Text content to analyze
            context: Optional context (timing data, source info, etc.)

        Returns:
            Complete ITP score structure
        """
        # Hash content
        content_hash = hashlib.sha256(content.encode()).hexdigest()

        # Calculate all 20 category scores
        categories = self._calculate_all_categories(content, context)

        # Calculate composite factors
        composite_factors = self._calculate_composite_factors(categories)

        # Calculate overall score
        overall_score = self._calculate_overall_score(composite_factors)

        # Generate response
        return {
            'version': self.VERSION,
            'content_hash': f"sha256:{content_hash}",
            'score': {
                'overall': overall_score,
                'confidence': self._calculate_confidence(categories),
                'composite_factors': composite_factors
            },
            'metadata': {
                'scorer': {
                    'type': 'ai',
                    'identifier': 'nci-reference-implementation',
                    'version': self.VERSION
                },
                'generated_at': self._get_timestamp(),
                'processing_time_ms': 0  # Placeholder
            }
        }

    def _calculate_all_categories(self, content: str, context: dict) -> Dict[str, Tuple[int, str]]:
        """Calculate all 20 category scores. Returns dict of (score, evidence) tuples."""
        return {
            # Emotional Manipulation composite
            'emotional_manipulation_base': self._calc_emotional_base(content),
            'call_for_urgent_action': self._calc_urgent_action(content),
            'overuse_of_novelty': self._calc_novelty(content),
            'emotional_repetition': self._calc_repetition(content),
            'manufactured_outrage': self._calc_outrage(content, context),

            # Suspicious Timing composite
            'timing': self._calc_timing(context),
            'financial_political_gain': self._calc_gain(content, context),
            'historical_parallels': self._calc_parallels(content, context),

            # Uniform Messaging composite
            'uniform_messaging_base': self._calc_uniform_messaging(content, context),
            'bandwagon_effect': self._calc_bandwagon(content),
            'rapid_behavior_shifts': self._calc_behavior_shifts(context),

            # Tribal Division composite
            'tribal_division_base': self._calc_tribal_division(content),
            'simplistic_narratives': self._calc_simplistic(content),
            'false_dilemmas': self._calc_false_dilemmas(content),

            # Missing Information composite
            'missing_information_base': self._calc_missing_info(content, context),
            'authority_overload': self._calc_authority(content, context),
            'suppression_of_dissent': self._calc_suppression(content, context),
            'cherry_picked_data': self._calc_cherry_picking(content),
            'logical_fallacies': self._calc_fallacies(content),
            'framing_techniques': self._calc_framing(content)
        }

    def _calculate_composite_factors(self, categories: Dict[str, Tuple[int, str]]) -> dict:
        """Calculate composite factor scores from category scores."""
        composite_factors = {}

        for composite_name, category_weights in self.WEIGHTS.items():
            weighted_sum = 0
            total_weight = 0
            category_details = {}

            for category_name, weight in category_weights.items():
                score, evidence = categories[category_name]
                weighted_sum += score * weight
                total_weight += weight
                category_details[category_name] = {
                    'value': score,
                    'weight': weight,
                    'evidence': evidence
                }

            composite_factors[composite_name] = {
                'composite_value': round(weighted_sum / total_weight, 2),
                'confidence': 0.80,  # Placeholder - calculate from data quality
                'categories': category_details
            }

        return composite_factors

    def _calculate_overall_score(self, composite_factors: dict) -> float:
        """Calculate overall 0-100 score from composite factors."""
        weighted_sum = 0

        for factor_name, factor_data in composite_factors.items():
            weight = self.COMPOSITE_WEIGHTS[factor_name]
            value = factor_data['composite_value']
            confidence = factor_data['confidence']
            weighted_sum += value * weight * confidence

        # Scale from 1-5 range to 0-100 range
        overall_score = (weighted_sum - 1) * 25
        return round(overall_score, 1)

    def _calculate_confidence(self, categories: Dict[str, Tuple[int, str]]) -> float:
        """Calculate overall confidence score."""
        # Placeholder implementation
        return 0.80

    def _get_timestamp(self) -> str:
        """Get ISO 8601 timestamp."""
        from datetime import datetime
        return datetime.utcnow().isoformat() + 'Z'

    # Category calculation methods (placeholder implementations)
    # In production, these would contain full NLP and analysis logic

    def _calc_emotional_base(self, content: str) -> Tuple[int, str]:
        """Calculate emotional manipulation base score."""
        # Placeholder: count emotional trigger words
        triggers = ['fear', 'outrage', 'shocking', 'terrifying', 'devastating']
        count = sum(content.lower().count(word) for word in triggers)
        score = min(5, max(1, count // 2 + 1))
        return (score, f"Emotional trigger density: {count} occurrences")

    def _calc_urgent_action(self, content: str) -> Tuple[int, str]:
        """Calculate call for urgent action score."""
        urgency_words = ['immediately', 'urgent', 'now', 'critical', 'emergency']
        count = sum(content.lower().count(word) for word in urgency_words)
        score = min(5, max(1, count + 1))
        return (score, f"Urgency language: {count} instances")

    # Additional calculation methods would follow similar pattern...
    # (Abbreviated for space - full implementation would include all 20 methods)

    def _calc_novelty(self, content: str) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_repetition(self, content: str) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_outrage(self, content: str, context: dict) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_timing(self, context: dict) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_gain(self, content: str, context: dict) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_parallels(self, content: str, context: dict) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_uniform_messaging(self, content: str, context: dict) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_bandwagon(self, content: str) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_behavior_shifts(self, context: dict) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_tribal_division(self, content: str) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_simplistic(self, content: str) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_false_dilemmas(self, content: str) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_missing_info(self, content: str, context: dict) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_authority(self, content: str, context: dict) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_suppression(self, content: str, context: dict) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_cherry_picking(self, content: str) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_fallacies(self, content: str) -> Tuple[int, str]:
        return (1, "Placeholder implementation")

    def _calc_framing(self, content: str) -> Tuple[int, str]:
        return (1, "Placeholder implementation")


# Example usage
if __name__ == "__main__":
    itp = ITPImplementation()

    content = """
    URGENT: Unprecedented crisis demands immediate action!
    Everyone agrees this is the worst disaster in history.
    You're either with us or against us.
    """

    result = itp.analyze(content)
    print(f"Overall ITP Score: {result['score']['overall']}")
    print(f"Confidence: {result['score']['confidence']}")
```

### Appendix B: Historical PSYOP Scoring Examples

#### Example 1: Nayirah Testimony (1990) - Overall Score: 88

**Context**: Testimony before Congressional Human Rights Caucus claiming Iraqi soldiers removed babies from incubators in Kuwait. Later revealed to be fabricated; witness was daughter of Kuwaiti ambassador, coached by PR firm Hill & Knowlton.

| Category | Score | Evidence |
|----------|-------|----------|
| **EMOTIONAL MANIPULATION (4.8)** | | |
| Emotional Manipulation Base | 5 | Extreme emotional triggers: babies, death, hospital invasion |
| Call for Urgent Action | 5 | Demanded immediate military intervention |
| Overuse of Novelty | 5 | "Unprecedented atrocity," "never seen before" |
| Emotional Repetition | 5 | Baby incubator story repeated across all media |
| Manufactured Outrage | 4 | Coordinated outrage campaign, limited fact-checking |
| **SUSPICIOUS TIMING (5.0)** | | |
| Timing | 5 | Testimony timed perfectly with Congressional vote on war authorization |
| Financial/Political Gain | 5 | Kuwait government paying PR firm; US military-industrial complex |
| Historical Parallels | 5 | Mirrors WWI "Rape of Belgium" atrocity propaganda |
| **UNIFORM MESSAGING (5.0)** | | |
| Uniform Messaging Base | 5 | Identical story across all major outlets, no variation |
| Bandwagon Effect | 5 | "Everyone knows," "all witnesses confirm" |
| Rapid Behavior Shifts | 5 | Immediate shift in public opinion within days |
| **TRIBAL DIVISION (4.1)** | | |
| Tribal Division Base | 5 | Iraqis portrayed as inhuman monsters vs. innocent Kuwaitis |
| Simplistic Narratives | 4 | Pure evil vs. pure innocence framework |
| False Dilemmas | 3 | "Support war or support baby killers" |
| **MISSING INFORMATION (5.0)** | | |
| Missing Information Base | 5 | Witness identity concealed; PR firm involvement hidden |
| Authority Overload | 5 | Unverified testimony treated as expert evidence |
| Suppression of Dissent | 5 | Skeptics labeled "Saddam apologists" |
| Cherry-Picked Data | 5 | Only supporting testimonies aired, contradicting evidence ignored |
| Logical Fallacies | 5 | Appeal to emotion, appeal to authority, hasty generalization |
| Framing Techniques | 5 | Story framed to make military intervention seem morally mandatory |

**Composite Factor Scores**: EM: 4.8, ST: 5.0, UM: 5.0, TD: 4.1, MI: 5.0
**Overall ITP Score**: 88 (Overwhelming signs of PSYOP)

---

#### Example 2: Tobacco Industry "Doubt" Campaign (1950s-1990s) - Overall Score: 82

**Context**: Multi-decade campaign to manufacture doubt about tobacco health risks, using front groups, questionable experts, and strategic messaging coordinated by tobacco companies.

| Category | Score | Evidence |
|----------|-------|----------|
| **EMOTIONAL MANIPULATION (3.2)** | | |
| Emotional Manipulation Base | 3 | Fear of "nanny state," loss of freedom |
| Call for Urgent Action | 2 | No urgent action demanded (slow campaign) |
| Overuse of Novelty | 3 | "New studies show no link" |
| Emotional Repetition | 4 | "More research needed" repeated endlessly |
| Manufactured Outrage | 4 | Outrage against "alarmist" health officials |
| **SUSPICIOUS TIMING (3.5)** | | |
| Timing | 3 | Campaigns timed with proposed regulations |
| Financial/Political Gain | 5 | Tobacco companies gained billions by delaying regulation |
| Historical Parallels | 3 | Similar to earlier lead industry tactics |
| **UNIFORM MESSAGING (4.8)** | | |
| Uniform Messaging Base | 5 | Identical talking points across all industry spokespeople |
| Bandwagon Effect | 4 | "Many scientists disagree" (manufactured consensus) |
| Rapid Behavior Shifts | 5 | Coordinated deployment of front groups and "experts" |
| **TRIBAL DIVISION (2.8)** | | |
| Tribal Division Base | 3 | "Anti-smoking zealots" vs. "reasonable people" |
| Simplistic Narratives | 3 | "Freedom vs. control" framing |
| False Dilemmas | 2 | Some nuance maintained for credibility |
| **MISSING INFORMATION (4.9)** | | |
| Missing Information Base | 5 | Industry research hidden, internal documents concealed |
| Authority Overload | 5 | Industry-funded "experts" with questionable credentials |
| Suppression of Dissent | 5 | Legitimate scientists attacked, defunded, discredited |
| Cherry-Picked Data | 5 | Only studies showing no harm publicized |
| Logical Fallacies | 5 | False equivalence, appeal to ignorance ("not proven") |
| Framing Techniques | 5 | Issue framed as "scientific controversy" not public health |

**Composite Factor Scores**: EM: 3.2, ST: 3.5, UM: 4.8, TD: 2.8, MI: 4.9
**Overall ITP Score**: 82 (Overwhelming signs of PSYOP)

---

#### Example 3: COVID Lab Leak Origin Suppression (2020-2021) - Overall Score: 70

**Context**: Coordinated efforts to dismiss and suppress discussion of laboratory origin hypothesis for SARS-CoV-2, including organized letter campaigns and social media censorship.

| Category | Score | Evidence |
|----------|-------|----------|
| **EMOTIONAL MANIPULATION (4.1)** | | |
| Emotional Manipulation Base | 4 | Fear of "racism," "conspiracy theories" |
| Call for Urgent Action | 5 | "Must stop dangerous misinformation immediately" |
| Overuse of Novelty | 3 | Some historical context to pandemics provided |
| Emotional Repetition | 4 | "Debunked conspiracy theory" repeated constantly |
| Manufactured Outrage | 5 | Rapid, coordinated outrage against lab leak proponents |
| **SUSPICIOUS TIMING (4.5)** | | |
| Timing | 5 | Coordinated response within days of outbreak |
| Financial/Political Gain | 5 | Researchers with conflict of interest, China diplomatic interests |
| Historical Parallels | 3 | Some parallels to other suppression campaigns |
| **UNIFORM MESSAGING (4.2)** | | |
| Uniform Messaging Base | 5 | Identical language in Lancet letter, media coverage |
| Bandwagon Effect | 4 | "Scientific consensus" claimed prematurely |
| Rapid Behavior Shifts | 3 | Fast but not instantaneous adoption |
| **TRIBAL DIVISION (4.8)** | | |
| Tribal Division Base | 5 | "Anti-Asian racists" vs. "responsible scientists" |
| Simplistic Narratives | 5 | "Science vs. conspiracy theorists" binary |
| False Dilemmas | 4 | "Accept natural origin or be conspiracy theorist" |
| **MISSING INFORMATION (3.9)** | | |
| Missing Information Base | 4 | Lab data, early cases, conflict of interest not disclosed |
| Authority Overload | 3 | Mix of qualified and compromised experts |
| Suppression of Dissent | 5 | Scientists silenced, social media posts removed |
| Cherry-Picked Data | 4 | Proximal origin paper emphasized, lab data ignored |
| Logical Fallacies | 4 | Ad hominem, guilt by association, appeal to authority |
| Framing Techniques | 3 | Strong framing but some counter-narratives permitted |

**Composite Factor Scores**: EM: 4.1, ST: 4.5, UM: 4.2, TD: 4.8, MI: 3.9
**Overall ITP Score**: 70 (Strong likelihood of manipulation)

---

#### Scoring Summary Table

| Event | EM | ST | UM | TD | MI | Overall |
|-------|----|----|----|----|----|----|
| Nayirah Testimony (1990) | 4.8 | 5.0 | 5.0 | 4.1 | 5.0 | 88 |
| Tobacco "Doubt" Campaign | 3.2 | 3.5 | 4.8 | 2.8 | 4.9 | 82 |
| COVID Lab Leak Suppression | 4.1 | 4.5 | 4.2 | 4.8 | 3.9 | 70 |

### Appendix C: Glossary

- **ITP**: Influence Tactics Protocol
- **PSYOP**: Psychological Operation
- **Category**: Individual manipulation technique measured on 1-5 scale (20 total categories)
- **Composite Factor**: Aggregation of related categories into five primary dimensions
- **Validator**: Entity (human or AI) that scores content
- **Consensus**: Aggregated agreement across multiple validators
- **Confidence**: Statistical certainty of score (0-0.95 scale)
- **Manipulation Score**: Overall 0-100 assessment of manipulation likelihood
- **Evidence**: Specific textual or behavioral indicators supporting a category score
- **Weight**: Relative importance of a category within its composite factor
- **Hash**: SHA-256 cryptographic fingerprint of content for unique identification

---

### Acknowledgments

The scoring framework was inspired by publicly discussed work by Chase Hughes on influence and behavioral analysis. The ITP is an independent specification, not affiliated with or endorsed by Chase Hughes or any related organizations.

---

**Protocol Version**: 1.1
**Status**: Draft Standard
**Last Updated**: 2026-03
**License**: MIT
**Maintainer**: Synapti.ai
**Contact**: daniel.bentes@synapti.ai

---

### Appendix D: Change Log

#### Version 0.1 (2025-11-18)

**Major Changes**:
- Expanded from 5 composite factors to full 20-category scoring system
- Aligned protocol specification with the established scoring system
- Added hierarchical scoring architecture (20 categories → 5 composites → 1 overall)
- Standardized all category scores to 1-5 scale (previously 0-5)
- Added comprehensive calculation methodologies for all 20 categories
- Updated data structures to support detailed and composite scoring
- Expanded historical examples to show all 20 category scores
- Added complete category-to-composite factor mapping table
- Updated visual representations for both standard and detailed views
- Enhanced implementation requirements to mandate all 20 categories

**Category Additions**:
- Call for Urgent Action (#2)
- Overuse of Novelty (#3)
- Emotional Repetition (#4)
- Manufactured Outrage (#5)
- Financial/Political Gain (#7)
- Historical Parallels (#8)
- Bandwagon Effect (#10)
- Rapid Behavior Shifts (#11)
- Simplistic Narratives (#13)
- False Dilemmas (#14)
- Authority Overload (#16)
- Suppression of Dissent (#17)
- Cherry-Picked Data (#18)
- Logical Fallacies (#19)
- Framing Techniques (#20)

**Breaking Changes**:
- JSON structure changed to include `composite_factors` with nested `categories`
- Category scoring scale changed from 0-5 to 1-5
- Overall score calculation formula updated to use all 20 categories
- Implementations MUST now calculate all 20 categories to be compliant

**Rationale**:
This update ensures full consistency between the protocol specification and the established scoring methodology. The 20-category system provides:
- Greater granularity and explainability
- Better coverage of manipulation techniques
- Improved accuracy through specialized category scoring
- Maintained backwards compatibility via composite factor structure
- Enhanced educational value for users learning manipulation patterns

---

#### Version 0.2 (2025-12-19)

**Scoring Methodology Enhancements**:

Three categories received enhanced calculation formulas to improve detection accuracy:

1. **Category 12 (Tribal Division)**: Added dehumanization detection
   - New component: `dehumanization_score` measuring dehumanizing language density
   - Dehumanizing terms (vermin, parasites, plague, etc.) are the strongest tribal indicator
   - Presence of dehumanization automatically elevates score to maximum (5)
   - Weight distribution changed from (0.4, 0.3, 0.3) to equal weights (0.25 × 4)

2. **Category 15 (Missing Information)**: Added attribution asymmetry detection
   - New component: `attribution_asymmetry` measuring biased source treatment
   - Detects when credible verbs (confirmed, proved) are used for favored sources
     while discrediting verbs (claimed, alleged) are used for disfavored sources
   - Formula changed from multiplication to weighted sum for better calibration
   - Asymmetry >0.7 adds +1 to score; >0.5 adds +0.5

3. **Category 20 (Framing Techniques)**: Added pattern matching criteria
   - New component: `pattern_detection` for explicit framing patterns
   - Six specific patterns defined: victim-villain-hero, false balance, scope manipulation,
     temporal framing, passive voice agency obscuring, loaded language
   - Makes abstract framing detection concrete and reproducible
   - Weight distribution changed to equal weights (0.25 × 4)

**Rationale**:
These enhancements were identified through implementation experience and improve:
- Specificity: Concrete patterns replace abstract formulas
- Reproducibility: Explicit term lists enable consistent scoring across implementations
- Sensitivity: New components detect manipulation techniques previously under-weighted

**Non-Breaking Changes**:
- All category numbers and names remain unchanged
- Composite factor weights remain unchanged
- Overall score calculation remains unchanged
- Existing implementations remain compliant (enhancements are additive)

---

#### Version 1.0 (2025-12-19)

**Protocol Specification Improvements**:

This version improves the specification document to align with RFC/IETF protocol standards best practices:

1. **RFC 2119 Compliance**
   - Added RFC 2119 terminology boilerplate after Abstract
   - Fixed keyword consistency (lowercase "must" → uppercase "MUST" where normative)
   - All normative requirements now use proper RFC 2119 keywords

2. **Conformance Levels (§8.0)**
   - Added three-tier conformance system: ITP-Core, ITP-Validated, ITP-Full
   - Implementations MUST declare conformance level via `X-ITP-Conformance-Level` header
   - Enables partial compliance while maintaining interoperability

3. **Error Response Specification (§4.3)**
   - Added structured error response format
   - Defined 9 standard error codes with HTTP status mappings
   - Added `Retry-After` header requirement for rate limiting

4. **Transport Security Requirements (§7.5)**
   - Added HTTPS requirement for API endpoints
   - Specified TLS version requirements (MUST: 1.2, SHOULD: 1.3)
   - Added certificate requirements

5. **JSON Schema Definitions (Appendix F)**
   - Added normative JSON Schema for Content Identifier
   - Added normative JSON Schema for Analysis Request
   - Added normative JSON Schema for ITP Score (with nested definitions)
   - Added normative JSON Schema for Error Response

6. **Calculation Methodology Clarification (Appendix G)**
   - Marked all §3.2 Calculation sections as informative (non-normative)
   - Implementations MAY use alternative calculation methods
   - Added validation guidance for alternative implementations

7. **References Section (§11)**
   - Added normative references: RFC 2119, RFC 8259, RFC 7231, RFC 3339, JSON Schema
   - Added informative references: OWASP API Security, TLS 1.3

8. **Specification Quality Refinements**
   - Defined maximum content length (100,000 characters) for `CONTENT_TOO_LONG` error
   - Updated JSON Schema with `maxLength` constraint
   - Clarified §8.1 relationship to Level 1 (ITP-Core) conformance
   - Enhanced Appendix G validation approach with specific metrics
   - Updated Implementation Checklist (Appendix E) with conformance, error handling, and security requirements

**Non-Breaking Changes**:
- All API endpoints remain unchanged
- All data structures remain backward compatible
- Existing compliant implementations remain compliant

---

### Appendix E: Implementation Checklist

Use this checklist to verify protocol compliance:

**Category Implementation**:
- [ ] Category 1: Emotional Manipulation (Base)
- [ ] Category 2: Call for Urgent Action
- [ ] Category 3: Overuse of Novelty
- [ ] Category 4: Emotional Repetition
- [ ] Category 5: Manufactured Outrage
- [ ] Category 6: Timing
- [ ] Category 7: Financial/Political Gain
- [ ] Category 8: Historical Parallels
- [ ] Category 9: Uniform Messaging (Base)
- [ ] Category 10: Bandwagon Effect
- [ ] Category 11: Rapid Behavior Shifts
- [ ] Category 12: Tribal Division (Base)
- [ ] Category 13: Simplistic Narratives
- [ ] Category 14: False Dilemmas
- [ ] Category 15: Missing Information (Base)
- [ ] Category 16: Authority Overload
- [ ] Category 17: Suppression of Dissent
- [ ] Category 18: Cherry-Picked Data
- [ ] Category 19: Logical Fallacies
- [ ] Category 20: Framing Techniques

**Composite Factors**:
- [ ] Emotional Manipulation (categories 1-5)
- [ ] Suspicious Timing (categories 6-8)
- [ ] Uniform Messaging (categories 9-11)
- [ ] Tribal Division (categories 12-14)
- [ ] Missing Information (categories 15-20)

**Data Structures**:
- [ ] Content Identifier with SHA-256 hash
- [ ] Complete ITP Score Structure with nested categories
- [ ] Perspective Structure
- [ ] Validation Structure
- [ ] Consensus Structure

**API Endpoints**:
- [ ] POST /v1/analyze
- [ ] GET /v1/score/{content_hash}
- [ ] POST /v1/validate (Level 2+)
- [ ] GET /v1/consensus/{content_hash} (Level 2+)

**Conformance (§8.0)**:
- [ ] Conformance level declared (1, 2, or 3)
- [ ] `X-ITP-Conformance-Level` header included in responses
- [ ] All requirements for declared level met

**Error Handling (§4.3)**:
- [ ] Structured error responses implemented
- [ ] All 9 standard error codes supported
- [ ] Correct HTTP status codes returned
- [ ] `Retry-After` header on 429 responses

**Transport Security (§7.5)**:
- [ ] HTTPS only (HTTP rejected)
- [ ] TLS 1.2 supported
- [ ] TLS 1.3 supported (recommended)

**Testing**:
- [ ] Protocol compliance test suite passes
- [ ] >70% accuracy on validation corpus
- [ ] Edge case handling verified
- [ ] Performance requirements met

### Appendix F: JSON Schema Definitions

These schemas define the normative structure for ITP data types. Implementations MUST validate data against these schemas.

#### F.1 Content Identifier Schema

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://raw.githubusercontent.com/synaptiai/influence-tactics-protocol/main/schemas/content-identifier.json",
  "title": "ITP Content Identifier",
  "type": "object",
  "required": ["content_hash", "content_type"],
  "properties": {
    "content_hash": {
      "type": "string",
      "pattern": "^sha256:[a-f0-9]{64}$",
      "description": "SHA-256 hash of content with 'sha256:' prefix"
    },
    "content_type": {
      "type": "string",
      "enum": ["text/plain", "text/html", "text/markdown"],
      "description": "MIME type of the content"
    },
    "content_length": {
      "type": "integer",
      "minimum": 50,
      "description": "Length of content in characters"
    },
    "platform": {
      "type": "string",
      "description": "Source platform identifier"
    },
    "url": {
      "type": "string",
      "format": "uri",
      "description": "Original URL of the content"
    },
    "timestamp": {
      "type": "string",
      "format": "date-time",
      "description": "ISO 8601 timestamp of content creation or retrieval"
    }
  }
}
```

#### F.2 Analysis Request Schema

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://raw.githubusercontent.com/synaptiai/influence-tactics-protocol/main/schemas/analysis-request.json",
  "title": "ITP Analysis Request",
  "type": "object",
  "required": ["content"],
  "properties": {
    "content": {
      "type": "string",
      "minLength": 50,
      "maxLength": 1000000,
      "description": "Text content to analyze (50-1,000,000 characters)"
    },
    "content_type": {
      "type": "string",
      "enum": ["text/plain", "text/html", "text/markdown"],
      "default": "text/plain"
    },
    "semantic_content_type": {
      "type": "string",
      "enum": ["auto", "news", "social_media"],
      "default": "auto",
      "description": "OPTIONAL content category hint for context-aware analysis routing"
    },
    "options": {
      "type": "object",
      "properties": {
        "include_evidence": {
          "type": "boolean",
          "default": true
        },
        "include_perspectives": {
          "type": "boolean",
          "default": false
        },
        "language": {
          "type": "string",
          "pattern": "^[a-z]{2}(-[A-Z]{2})?$",
          "description": "BCP 47 language tag"
        }
      }
    }
  }
}
```

#### F.3 ITP Score Schema

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://raw.githubusercontent.com/synaptiai/influence-tactics-protocol/main/schemas/itp-score.json",
  "title": "ITP Score",
  "type": "object",
  "required": ["version", "content_hash", "score"],
  "properties": {
    "version": {
      "type": "string",
      "pattern": "^\\d+\\.\\d+$",
      "description": "Protocol version"
    },
    "content_hash": {
      "type": "string",
      "pattern": "^sha256:[a-f0-9]{64}$"
    },
    "score": {
      "type": "object",
      "required": ["overall", "confidence", "composite_factors"],
      "properties": {
        "overall": {
          "type": "number",
          "minimum": 0,
          "maximum": 100,
          "description": "Overall ITP score (0-100)"
        },
        "confidence": {
          "type": "number",
          "minimum": 0,
          "maximum": 1,
          "description": "Confidence level (0-1)"
        },
        "composite_factors": {
          "type": "object",
          "required": [
            "emotional_manipulation",
            "suspicious_timing",
            "uniform_messaging",
            "tribal_division",
            "missing_information"
          ],
          "additionalProperties": {
            "$ref": "#/$defs/compositeFactor"
          }
        },
        "risk_tier": {
          "type": "string",
          "enum": ["LOW", "MODERATE", "HIGH", "SEVERE"],
          "description": "OPTIONAL human-readable risk classification"
        },
        "risk_emoji": {
          "type": "string",
          "description": "OPTIONAL visual indicator emoji"
        },
        "risk_indicator": {
          "type": "string",
          "description": "OPTIONAL text indicator (·, !, !!, !!!)"
        }
      }
    },
    "metadata": {
      "type": "object",
      "properties": {
        "scorer": {
          "type": "object",
          "required": ["type", "identifier"],
          "properties": {
            "type": {"type": "string", "enum": ["ai", "human", "oracle"]},
            "identifier": {"type": "string"},
            "version": {"type": "string"}
          }
        },
        "generated_at": {"type": "string", "format": "date-time"},
        "processing_time_ms": {"type": "integer", "minimum": 0}
      }
    }
  },
  "$defs": {
    "compositeFactor": {
      "type": "object",
      "required": ["composite_value", "confidence", "categories"],
      "properties": {
        "composite_value": {
          "type": "number",
          "minimum": 1,
          "maximum": 5
        },
        "confidence": {
          "type": "number",
          "minimum": 0,
          "maximum": 1
        },
        "categories": {
          "type": "object",
          "additionalProperties": {
            "$ref": "#/$defs/category"
          }
        }
      }
    },
    "category": {
      "type": "object",
      "required": ["value", "weight"],
      "properties": {
        "value": {
          "type": "integer",
          "minimum": 1,
          "maximum": 5
        },
        "weight": {
          "type": "number",
          "minimum": 0,
          "maximum": 1
        },
        "evidence": {
          "type": "string"
        }
      }
    }
  }
}
```

#### F.4 Error Response Schema

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://raw.githubusercontent.com/synaptiai/influence-tactics-protocol/main/schemas/error-response.json",
  "title": "ITP Error Response",
  "type": "object",
  "required": ["error", "status"],
  "properties": {
    "error": {
      "type": "object",
      "required": ["code", "message"],
      "properties": {
        "code": {
          "type": "string",
          "enum": [
            "INVALID_REQUEST",
            "CONTENT_TOO_SHORT",
            "CONTENT_TOO_LONG",
            "INVALID_CONTENT_TYPE",
            "INVALID_CONTENT_HASH",
            "CONTENT_NOT_FOUND",
            "VALIDATION_NOT_FOUND",
            "RATE_LIMIT_EXCEEDED",
            "INTERNAL_ERROR"
          ]
        },
        "message": {
          "type": "string",
          "description": "Human-readable error description"
        },
        "details": {
          "type": "object",
          "description": "Additional error context"
        }
      }
    },
    "status": {
      "type": "string",
      "const": "error"
    }
  }
}
```

#### F.5 Consensus Response Schema

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "$id": "https://raw.githubusercontent.com/synaptiai/influence-tactics-protocol/main/schemas/consensus-response.json",
  "title": "ITP Consensus Response",
  "type": "object",
  "required": ["content_hash", "consensus", "status"],
  "properties": {
    "content_hash": {
      "type": "string",
      "pattern": "^sha256:[a-f0-9]{64}$"
    },
    "consensus": {
      "type": "object",
      "required": [
        "consensus_score",
        "ai_score",
        "human_score",
        "confidence",
        "confidence_interval",
        "validation_count",
        "is_valid"
      ],
      "properties": {
        "consensus_score": {
          "type": "number",
          "minimum": 0,
          "maximum": 100,
          "description": "Final weighted consensus score"
        },
        "ai_score": {
          "type": "number",
          "minimum": 0,
          "maximum": 100,
          "description": "AI-generated score component"
        },
        "human_score": {
          "type": "number",
          "minimum": 0,
          "maximum": 100,
          "description": "Reputation-weighted average of human validator scores"
        },
        "confidence": {
          "type": "number",
          "minimum": 0,
          "maximum": 1,
          "description": "Overall confidence in the consensus"
        },
        "confidence_interval": {
          "type": "object",
          "required": ["lower", "upper"],
          "properties": {
            "lower": {
              "type": "number",
              "minimum": 0,
              "maximum": 100
            },
            "upper": {
              "type": "number",
              "minimum": 0,
              "maximum": 100
            }
          }
        },
        "validation_count": {
          "type": "integer",
          "minimum": 0,
          "description": "Number of human validations included"
        },
        "is_valid": {
          "type": "boolean",
          "description": "Whether consensus meets minimum validity criteria"
        }
      }
    },
    "status": {
      "type": "string",
      "const": "success"
    }
  }
}
```

### Appendix G: Calculation Methodology (Informative)

This appendix is **informative** (non-normative). It provides guidance on the reference calculation methodology used in §3.2. Implementations are NOT required to use these specific formulas.

#### G.1 Purpose of Reference Calculations

The **Calculation** sections in §3.2 serve as reference implementations to:
- Illustrate one valid approach to scoring each category
- Provide baseline behavior for test suite validation
- Guide implementers who prefer a structured starting point

#### G.2 Interoperability Requirements

For interoperability, implementations MUST:
- Produce integer scores in the range 1-5 for each category
- Produce composite factor scores in the range 1.0-5.0
- Produce overall scores in the range 0-100
- Produce confidence values in the range 0-1

Implementations MAY:
- Use machine learning models instead of formula-based approaches
- Use different weighting schemes
- Employ alternative linguistic analysis techniques
- Combine multiple methodologies

#### G.3 Reference Implementation Notes

The reference formulas in §3.2 use a common structure:

```
score = w1 * factor1 + w2 * factor2 + w3 * factor3
```

Where weights (w1, w2, w3) typically sum to 1.0. The default weights provided are suggestions based on empirical testing and MAY be adjusted by implementations.

#### G.4 Validation Approach

Implementations using alternative calculation methods SHOULD validate their approach by:
1. Creating a validation corpus of at least 100 diverse content samples with known manipulation characteristics
2. Comparing scores against the reference formulas in §3.2 or another validated implementation
3. Achieving Pearson correlation ≥0.8 with reference scores across all categories
4. Maintaining consistent score distributions (standard deviation within 20% of reference)

**Note**: A standardized test corpus with ground truth scores MAY be published by the protocol maintainers as an informative companion resource. Until such a corpus is available, implementations SHOULD document their validation methodology.

This validation ensures alternative implementations produce compatible results while allowing methodological flexibility.
