# Voice Agents Vocabulary

**W3C AI Knowledge Representation Community Group — Draft Community Group Report**

**Status:** Draft Community Group Report — W3C AI Knowledge Representation Community Group (AI KR CG)

> This specification was published by the AI Knowledge Representation Community Group. It is **not a W3C Standard nor is it on the W3C Standards Track**. Please note that under the [W3C Community Contributor License Agreement (CLA)](https://www.w3.org/community/about/agreements/cla/) there is a limited opt-out and other conditions apply. Learn more about [W3C Community and Business Groups](https://www.w3.org/community/).
>
> This is a **DRAFT COMMUNITY REPORT**, open for participants contributions on June 2 2026. Contributors can contact the chair or post to the CG list directly to suggest edits and amendments.
>
> GitHub Issues are preferred for discussion of this specification. Alternatively, send comments to public-aikr@w3.org — archives at [lists.w3.org/Archives/Public/public-aikr/](https://lists.w3.org/Archives/Public/public-aikr/). Source repository: [https://github.com/w3c-cg/aikr](https://github.com/w3c-cg/aikr).

## Abstract

This document proposes a baseline vocabulary of terms for agentic voice interaction,
for contribution to the W3C AI Knowledge Representation Community Group (AI KR CG)
and, where relevant, the W3C Smart Voice Agents initiative. It is structured under the
CG's own eight-category Agentic AI Knowledge-Domains taxonomy so that it can be
merged into the CG's existing 148-term Agentic AI Vocabulary without duplicating it.

## Editorial note on scope and method

Terms already defined in the CG's Agentic
AI Vocabulary (e.g. ReactiveAgent, human-in-the-loop,
MCP) are cross-referenced by relation rather than redefined here.
Sections 1-8 below follow the CG's locked
[Knowledge-Domains taxonomy](https://w3c-cg.github.io/aikr/taxonomy/) exactly, in
category order, so new terms can be merged directly into the corresponding sections of the
main vocabulary. This draft additionally carries three non-normative appendices, added to
close specific coverage gaps identified during review:


Appendix A (Implementation-layer vocabulary) — parsed directly from four
widely used open-source voice-agent frameworks (`livekit/agents`,
`TEN-framework/ten-framework`, `pipecat-ai/pipecat`,
`vocodedev/vocode-core`). Each definition is a novel restatement aligned
with — but not copied from — the cited repository's own README.
Appendix B (Book-sourced design vocabulary) — terms from the editor's
unpublished Voice AI book manuscript (working chapters on the "Voice Kit Vision" and the CRUX
design framework). These are the editor's own original terminology, included for completeness
of the CG's voice-agent conceptual coverage; they are not yet externally published or
peer-reviewed, and should be flagged as such on submission.
Appendix C (Workshop-sourced vocabulary) — terms drawn from the eight
cross-cutting issues identified in the official W3C Workshop on
Smart Voice Agents report (25-27 February 2026; published 31 March 2026). This is the
most authoritative and current external source in this draft and should anchor any near-term CG
submission.

## Contents

1. [Agent types & autonomy](#1-agent-types-autonomy) (5)
2. [Cognition & capability](#2-cognition-capability) (10)
3. [Interaction, communication & identity](#3-interaction-communication-identity) (15)
4. [Commerce & settlement](#4-commerce-settlement) (3)
5. [Oversight, safety & interpretability](#5-oversight-safety-interpretability) (5)
6. [Regulation & governance](#6-regulation-governance) (4)
7. [Agentic standards & standards bodies](#7-agentic-standards-standards-bodies) (7)
8. [Applied domains](#8-applied-domains) (5)
9.A [Implementation-layer vocabulary (parsed from open-source repositories)](#appendix-a) (13)
9.B [Design vocabulary from the Voice AI book (Di Maio, unpublished manuscript)](#appendix-b) (7)
9.C [Vocabulary from the W3C Smart Voice Agents Workshop Report (Feb 2026)](#appendix-c) (19)

## 1. Agent types & autonomy (5)

| Term | Proposed definition | Source | Relations |
|---|---|---|---|
| **VoiceAgent** | Agent whose primary interaction modality is spoken language, typically combining ASR, an LLM reasoning core, and TTS in a real-time loop. | AI-KR CG working definition, informed by voice-agent architecture literature | broader: agent; related: ConversationalAgent |
| **Full-duplex voice agent** | Voice agent architected to listen and speak concurrently on independent audio streams, enabling natural overlap and immediate barge-in rather than strict turn-by-turn exchange. | Full-Duplex-Bench [FDBENCH]; τ-Voice [TAUVOICE] | broader: VoiceAgent; related: barge-in, turn-taking |
| **Half-duplex voice agent** | Voice agent that enforces strict alternating turns, only listening after it has finished speaking; simpler to build but less natural under interruption. | AI-KR CG working definition | broader: VoiceAgent; contrast: Full-duplex voice agent |
| **Speech-first agent** | Agent designed with voice as the default and primary interface rather than as a bolt-on channel to a text-based assistant. | AI-KR CG working definition | broader: VoiceAgent |
| **Telephony agent** | Voice agent deployed over PSTN/SIP telephony rather than a browser or app microphone, subject to narrowband audio and carrier-network constraints. | AI-KR CG working definition | broader: VoiceAgent; related: MRCP |

## 2. Cognition & capability (10)

| Term | Proposed definition | Source | Relations |
|---|---|---|---|
| **ASR (Automatic Speech Recognition)** | The capability that converts an acoustic speech signal into a text transcript, streamed incrementally in real-time voice agents. | W3C Web Speech API [WEB-SPEECH-API] | broader: Perception; related: endpointing |
| **TTS (Text-to-Speech)** | The capability that synthesizes spoken audio from text, typically via a neural vocoder, including prosody and voice-identity control. | W3C Web Speech API [WEB-SPEECH-API]; SSML | broader: capability; related: SSML, prosody |
| **VAD (Voice Activity Detection)** | The capability that distinguishes speech from silence or non-speech audio in a stream, gating when ASR and downstream processing engage. | Silero VAD, cited in [TURNEOT] | broader: Perception; related: endpointing, barge-in |
| **Endpointing** | The decision process that determines when a user has finished a spoken turn, triggering the agent's response; may be fixed-silence, prosody-based, or semantic/model-based. | [TURNEOT]; Li, Paranjape & Manning (arXiv:2208.03812) | broader: Cognition & capability; related: VAD, turn-taking |
| **Barge-in** | The agent capability to detect that a user has begun speaking while the agent's own TTS is playing, and to immediately halt playback and cancel in-flight generation. | Voice Agent Architecture (Baby, 2026); [IHBENCH] | broader: Interaction, communication & identity; related: endpointing, echo cancellation |
| **Turn-taking** | The joint mechanism by which a voice agent and a user negotiate who speaks next, including timing of initiation, yielding, and permitted overlap. | Skantze & Irfan (arXiv:2501.08946); Talking Turns (arXiv:2503.01174) | broader: Cognition & capability; related: barge-in, endpointing |
| **Prosody** | The rhythm, stress, pitch, and intonation pattern of synthesized or recognized speech, distinct from its lexical content; a key driver of perceived naturalness. | AI voice latency and naturalness literature (industry + academic) | broader: TTS |
| **Speaker diarization** | The process of partitioning an audio stream by speaker identity ('who spoke when'), used in multi-party voice-agent scenarios. | General speech-processing literature | broader: Perception |
| **Wake-word detection** | A lightweight, always-listening capability that detects a designated trigger phrase to activate full voice-agent processing, balancing responsiveness against privacy and power draw. | General speech-processing literature | broader: Perception; related: VAD |
| **Echo cancellation (AEC)** | Signal-processing capability that removes an agent's own synthesized speech from its microphone input, preventing self-triggered feedback loops during full-duplex operation. | WebRTC AEC; Voice Agent Architecture (Baby, 2026) | broader: Cognition & capability; related: barge-in |

## 3. Interaction, communication & identity (15)

| Term | Proposed definition | Source | Relations |
|---|---|---|---|
| **SSML (Speech Synthesis Markup Language)** | A W3C markup vocabulary for controlling pronunciation, prosody, and pacing in synthesized speech output. | [SSML10] | broader: TTS |
| **VoiceXML** | A W3C markup language for building interactive telephony-style voice dialogues (menus, prompts, grammars, form-filling). | [VOICEXML21] | related: MRCP, telephony agent |
| **EMMA (Extensible MultiModal Annotation)** | A W3C markup format for representing interpretations of user input (including speech) with confidence, timestamps, and alternatives, for exchange between input processors and interaction managers. | [EMMA20] | related: ASR, VoiceInteractionState |
| **MRCP (Media Resource Control Protocol)** | A protocol that lets a voice-application server control speech resources (ASR/TTS engines) hosted elsewhere on the network, common in telephony IVR deployments. | [MRCPV2] | related: telephony agent, VoiceXML |
| **VoiceInteractionState** | A proposed enumerated state (e.g., idle / listening / thinking / speaking / interrupted) representing where a voice agent currently sits in its interaction cycle. | AI-KR CG voiceAI drafts (voice-ai-standards-withnewtypes.html) | broader: state machine; related: VoiceInteractionStateMachine |
| **VoiceInteractionStateMachine** | A proposed interface exposing the current and permitted-next VoiceInteractionState values, allowing an application to react to and drive voice-agent turn transitions. | AI-KR CG voiceAI drafts (voice-ai-standards-withnewtypes.html) | related: VoiceInteractionState, turn-taking |
| **VoiceContext** | A proposed interface carrying accumulated dialogue/session state (slots, history, user profile) available to a voice agent across turns. | AI-KR CG voiceAI drafts (voice-ai-standards-withnewtypes.html) | related: VoiceHistoryEntry |
| **VoicePlaybackController** | A proposed interface for temporal control (pause, resume, cancel, seek) of in-progress TTS playback, distinct from stopping the underlying audio element. | AI-KR CG voiceAI drafts (voice-ai-standards-withnewtypes.html) | related: barge-in |
| **VoiceSessionRecovery** | A proposed interface and protocol for resuming a voice session after disconnection or interruption without discarding prior context or repeating already-delivered content. | AI-KR CG voiceAI drafts (voice-ai-standards-withnewtypes.html); [IHBENCH] | related: VoiceHistoryEntry, VoiceContext |
| **Voice biometrics / speaker verification** | The use of voice-derived features to authenticate or verify the identity of a speaker, distinct from ASR content recognition. | Sardine 'AI Fraud Vectors' 2026; Fintech Global 2026 | related: liveness detection, voice cloning |
| **VoiceTask** | A proposed interface representing a single unit of background work (e.g. a lookup, a booking action) that a voice agent has queued for asynchronous execution while the spoken conversation continues. | AI-KR CG voiceAI drafts (voice-ai-standards-withnewtypes.html); Di Maio Voice AI book manuscript, Ch.4 'Background Processing' | related: VoiceTaskQueue, VoiceTaskStatus |
| **VoiceTaskQueue** | A proposed interface managing an ordered set of VoiceTask instances awaiting or in execution, letting a voice agent report progress on background work without blocking the conversational turn. | AI-KR CG voiceAI drafts (voice-ai-standards-withnewtypes.html); Di Maio Voice AI book manuscript, Ch.4 'Background Processing' | related: VoiceTask, VoiceTaskCallback |
| **VoiceTaskStatus** | A proposed enumerated state (e.g. queued / running / done / failed) describing where a VoiceTask currently sits in its execution lifecycle. | AI-KR CG voiceAI drafts (voice-ai-standards-withnewtypes.html) | related: VoiceTask |
| **VoiceTaskResult** | A proposed interface carrying the outcome of a completed VoiceTask, for the agent to summarize back to the user at an appropriate conversational moment. | AI-KR CG voiceAI drafts (voice-ai-standards-withnewtypes.html) | related: VoiceTask, VoiceTaskStatus |
| **VoiceTaskCallback** | A proposed callback interface invoked when a VoiceTask changes status, letting an application surface background-task progress (e.g. 'still working on that booking') during an ongoing voice session. | AI-KR CG voiceAI drafts (voice-ai-standards-withnewtypes.html) | related: VoiceTaskQueue, VoiceTaskStatus |

## 4. Commerce & settlement (3)

| Term | Proposed definition | Source | Relations |
|---|---|---|---|
| **Conversational commerce** | Purchases, bookings, or account transactions initiated and completed through a spoken dialogue with a voice agent rather than a visual UI. | Industry usage; general voice-commerce literature | broader: Commerce & settlement |
| **Voice-authorized payment** | A payment or transfer for which spoken confirmation (optionally paired with voice biometric verification) constitutes part of the authorization chain. | Industry usage; general voice-commerce literature | related: voice biometrics |
| **IVR payment (PCI DSS scope)** | Interactive-voice-response capture of card or account details, a channel subject to PCI DSS de-scoping and secure-capture requirements distinct from web/app payment flows. | PCI Security Standards Council guidance (general) | related: telephony agent, MRCP |

## 5. Oversight, safety & interpretability (5)

| Term | Proposed definition | Source | Relations |
|---|---|---|---|
| **Voice deepfake / voice cloning** | Synthetic audio generated to mimic a specific person's voice, used both legitimately (personalized TTS) and adversarially (impersonation, fraud). | Sardine 'AI Fraud Vectors' 2026; fintech.global 2026 | related: liveness detection, voice biometrics |
| **Liveness detection (voice)** | Techniques that distinguish a live human speaker from a replayed, synthetic, or deepfaked audio stream during authentication. | Fintech Global 2026; Sardine 'AI Fraud Vectors' 2026 | related: voice biometrics, voice deepfake |
| **Spoken hallucination** | An ASR/LLM pipeline producing a fluent but factually or contextually incorrect spoken response, a voice-specific instance of model hallucination compounded by transcription error. | General LLM/voice-agent evaluation literature | related: WER, agent-as-judge |
| **WER (Word Error Rate)** | The standard metric for ASR transcription accuracy; a necessary but insufficient measure of voice-agent quality, as it does not capture turn-taking, latency, or task success. | How to Evaluate Voice AI Agents (industry practitioner literature) | related: Task Success Rate |
| **Task Success Rate (TSR)** | The percentage of voice-agent interactions that meet defined goal and constraint criteria, used as an outcome-level evaluation metric distinct from transcription accuracy. | How to Evaluate Voice AI Agents (industry practitioner literature) | related: WER |

## 6. Regulation & governance (4)

| Term | Proposed definition | Source | Relations |
|---|---|---|---|
| **AI voice disclosure obligation** | A regulatory requirement (e.g., EU AI Act Article 50 transparency obligations) that a person interacting with a voice system be informed they are speaking with an AI, absent an applicable exemption. | EU AI Act, Article 50 (general reference; cf. AI-KR CG vocabulary 'Article 51/53') | related: EU AI Act |
| **FCC AI-voice robocall rule** | US Federal Communications Commission rulemaking treating AI-generated voice calls under existing robocall/TCPA consent requirements. | FCC declaratory ruling (general reference) | related: telephony agent |
| **Voice call recording consent law** | Jurisdiction-dependent (one-party vs. two-party/all-party consent) legal requirement governing whether a voice agent may record a call, relevant to session logging and model training. | General wiretapping/consent-law reference (jurisdiction-dependent) | related: VoiceContext |
| **Accessibility conformance (voice)** | Requirements (e.g., WCAG success criteria touching audio alternatives, timing adjustable, and non-text contrast for visual voice-UI companions) that a voice interface must meet for users with disabilities. | [WCAG22] | related: W3C Voice Interaction |

## 7. Agentic standards & standards bodies (7)

| Term | Proposed definition | Source | Relations |
|---|---|---|---|
| **W3C Voice Interaction (Smart Voice Agents) initiative** | W3C activity and workshop track (Smart Voice Agents Workshop, October 2025) exploring standardization needs for voice-driven agentic interfaces on the Web. | W3C Smart Voice Agents Workshop | related: AI-KR CG voiceAI drafts |
| **W3C Web Speech API** | A W3C/WHATWG specification exposing browser-native speech recognition and speech synthesis to web applications. | [WEB-SPEECH-API] | related: ASR, TTS |
| **W3C SSML / VoiceXML / EMMA family** | The existing W3C Voice Browser Working Group specification family (SSML, VoiceXML, EMMA, PLS, SRGS) that any new agentic voice vocabulary must position itself relative to. | W3C Voice Browser Working Group | related: SSML, VoiceXML, EMMA |
| **MRCPv2** | IETF specification for the Media Resource Control Protocol used in telephony-integrated speech deployments. | [MRCPV2] | related: MRCP, telephony agent |
| **W3C Autonomous Agents on the Web (WebAgents) CG** | W3C Community Group on Web-based multi-agent systems, named by the Smart Voice Agents Workshop report as one of four relevant standardization homes for voice-agent interoperability work. | [SVAREPORT] | related: W3C AI Agent Protocol CG |
| **W3C Semantic 3D Content Accessibility CG** | W3C Community Group developing metadata and structural conventions to make three-dimensional and immersive web content legible to assistive technology, including voice agents; named by the Smart Voice Agents Workshop report as relevant to the accessibility gap it identified. | [SVAREPORT] | related: Semantic 3D content accessibility, embeddable voice agent |
| **Open Voice Interoperability Initiative (OVON)** | The originating body for the Open Floor Protocol, developing standards for coordinating turn-taking and floor control across independently built voice agents and human participants sharing a conversation. | [SVAREPORT] | related: Open Floor Protocol |

## 8. Applied domains (5)

| Term | Proposed definition | Source | Relations |
|---|---|---|---|
| **Call-center automation** | Deployment of voice agents to handle inbound/outbound contact-center interactions, often measured against human-agent baselines for AHT and CSAT. | Industry literature; general contact-center automation sources | related: Task Success Rate |
| **Voice banking / IVR banking** | Telephony- or app-based spoken interaction for account inquiries, transfers, and card servicing, a channel with distinct fraud and authentication considerations. | General fintech/voice-banking literature | related: voice biometrics, IVR payment |
| **Oral assessment / voice interview** | Use of voice agents to conduct structured spoken examinations or interviews, requiring turn-taking that tolerates thinking pauses and downstream transcript grading. | [ORALVOICE] | related: endpointing, WER |
| **Accessibility voice assistance** | Voice-agent deployment specifically to support users with visual, motor, or literacy-related access needs. | General accessibility literature; [WCAG22] | related: Accessibility conformance (voice) |
| **Automotive voice assistant** | In-cabin voice agent operating under far-field, road-noise, and safety-critical latency constraints distinct from handset or desktop deployments. | General automotive voice-agent literature | related: VAD, barge-in |

## Appendix A: Implementation-layer vocabulary (parsed from open-source repositories) (13) {#appendix-a}

| Term | Proposed definition | Source | Relations |
|---|---|---|---|
| **Agent (LiveKit usage)** | In LiveKit's runtime model, the configured unit of instructions and capabilities that gets invoked to handle a turn — distinct from the session or process that hosts it. | `github.com/livekit/agents` README | related: AgentSession |
| **AgentSession** | The runtime object that owns a single end-user interaction lifecycle, wiring VAD, STT, LLM, and TTS components together and mediating turn state for the Agent(s) running within it. | `github.com/livekit/agents` README | related: Agent, entrypoint |
| **entrypoint (session)** | The function invoked once per incoming session or job — analogous to a web server's request handler — from which an AgentSession and its Agent(s) are constructed and started. | `github.com/livekit/agents` README | related: AgentSession, AgentServer/Worker |
| **AgentServer / Worker process** | The long-running process that accepts incoming jobs (calls/sessions), applies scheduling, and spawns a per-session AgentSession to handle each one. | `github.com/livekit/agents` README | related: entrypoint |
| **Extension (TEN usage)** | A modular, independently swappable component — e.g. an STT, LLM, TTS, VAD, or turn-detection implementation — that plugs into a voice-agent Graph without requiring changes to the surrounding pipeline. | `github.com/TEN-framework/ten-framework` README | related: Graph (voice-agent) |
| **Graph (voice-agent, TEN usage)** | The declarative wiring of Extensions into a running voice-agent pipeline, analogous to a signal-flow diagram, that a TEN-based runtime executes. | `github.com/TEN-framework/ten-framework` README | related: Extension |
| **Pipeline (Pipecat usage)** | An ordered, composable chain of Frame Processors through which audio, text, and control data flow; the core execution unit of a Pipecat voice agent. | `github.com/pipecat-ai/pipecat` README | related: Frame, Processor |
| **Frame (Pipecat usage)** | The atomic unit of data — an audio chunk, a partial transcript, an LLM token, or a control signal — passed between Processors along a Pipeline. | `github.com/pipecat-ai/pipecat` README | related: Pipeline, Processor |
| **Frame Processor** | A single-responsibility stage in a Pipeline (e.g. an STT, LLM, or TTS service) that consumes and/or emits Frames. | `github.com/pipecat-ai/pipecat` README | related: Frame, Pipeline |
| **Transport (Pipecat usage)** | The Pipeline stage responsible for moving audio/video between the pipeline and the outside world over a specific medium (WebRTC, WebSocket, telephony), decoupling pipeline logic from connection technology. | `github.com/pipecat-ai/pipecat` README | related: Pipeline, telephony agent |
| **Serializer (Pipecat usage)** | A component that translates between a pipeline's internal Frame representation and a specific telephony/PBX provider's wire protocol (e.g. Twilio, Genesys, Plivo media streams). | `github.com/pipecat-ai/pipecat` README | related: Transport, telephony agent |
| **Speech-to-Speech (S2S) service** | A single integrated model or service that performs recognition, reasoning, and synthesis in one hop (e.g. a realtime multimodal API), as an alternative to composing separate STT, LLM, and TTS Processors. | `github.com/pipecat-ai/pipecat` README (services table) | related: ASR, TTS, Full-duplex voice agent |
| **StreamingConversation** | Vocode's core abstraction for a real-time, full-duplex spoken exchange between a user and an LLM-backed agent, coordinating streaming STT input and streaming TTS output over a single call/session object. | `github.com/vocodedev/vocode-core` README | related: Full-duplex voice agent, AgentSession |

## Appendix B: Design vocabulary from the Voice AI book (Di Maio, unpublished manuscript) (7) {#appendix-b}

| Term | Proposed definition | Source | Relations |
|---|---|---|---|
| **CRUX Framework** | Control, Respect, User-Centered, eXcellence — a four-part design framework proposed in the book for evaluating whether a voice interaction respects user agency, rather than only whether it works technically. | Di Maio, Voice AI book manuscript (unpublished; Chapter 3, 'Standards' / conversational AI standards roadmap) | related: Configuration Over Assumption |
| **Configuration Over Assumption** | The book's stated core design principle: rather than a voice agent assuming a single 'correct' interaction pace or style, the system exposes timing, interruption-handling, and interaction-pattern choices as user-configurable settings. | Di Maio, Voice AI book manuscript (unpublished; Chapter 4, 'Voice Kit Vision') | related: Deep Thinking Mode, Quick Exchange Mode, CRUX Framework |
| **Deep Thinking Mode** | A configurable voice-interaction mode prioritizing minimal interruption, extended silence tolerance, and support for non-linear exploration of half-formed ideas. | Di Maio, Voice AI book manuscript (unpublished; Chapter 4, 'Configurable Interaction Modes') | related: Configuration Over Assumption; contrast: Quick Exchange Mode |
| **Quick Exchange Mode** | A configurable voice-interaction mode optimized for short, rapid, transactional turns, contrasted with Deep Thinking Mode in the book's mode taxonomy. | Di Maio, Voice AI book manuscript (unpublished; Chapter 4, 'Configurable Interaction Modes') | related: Configuration Over Assumption; contrast: Deep Thinking Mode |
| **Thinking Space ('Hold on' mode)** | A user-invocable state in which the agent suspends response generation while the user composes a longer or more complex thought aloud — distinct from ordinary barge-in because the user is signalling 'not finished' rather than interrupting the agent. | Di Maio, Voice AI book manuscript (unpublished; Chapter 4, 'Interaction Control') | related: barge-in, turn-taking |
| **Limited Voice Options (anti-cloning pattern)** | A safety design pattern in which a voice agent's TTS output is restricted to a small, preset roster of synthetic voices specifically to prevent the system being used to clone or impersonate a real person's voice. | Di Maio, Voice AI book manuscript (unpublished; technical-stack notes, citing Anthropic voice-safety design practice) | related: voice cloning, deepfake detection (AI-KR CG financial-fraud vocabulary) |
| **Voice-to-text-to-voice gap** | The loss of conversational context and continuity that occurs when a user's interaction crosses between a voice channel and a text/visual channel of the same underlying assistant; treated in the book as a distinct usability failure mode rather than a minor implementation detail. | Di Maio, Voice AI book manuscript (unpublished; Chapter 3.4, 'Integration: Seamless Cross-Modal Experience') | related: VoiceContext, VoiceSessionRecovery |

## Appendix C: Vocabulary from the W3C Smart Voice Agents Workshop Report (Feb 2026) (19) {#appendix-c}

| Term | Proposed definition | Source | Relations |
|---|---|---|---|
| **Phonetic markup (voice agents)** | Markup specifying how a text string should be pronounced (e.g. an IPA override), flagged by the workshop as an unresolved shared-standard gap for proper names, abbreviations, and dialect-specific pronunciation. | [SVAREPORT] | related: SSML; Issue 1, pronunciation & language representation |
| **Dialect variation handling** | The unresolved standards gap around how a voice agent should represent, select, or switch between regional or dialect pronunciations and forms of the same language. | [SVAREPORT] | related: phonetic markup; Issue 1 |
| **Author pronunciation control** | The ability for a content author — rather than the end user or platform — to specify how their own name, brand, or terminology should be pronounced by a voice agent reading it aloud. | [SVAREPORT] | related: phonetic markup; Issue 1 |
| **Combined ASR+LLM error mode** | An error class specific to voice agents in which a transcription mistake and a downstream LLM reasoning mistake compound each other, distinct from either a pure ASR error or a pure text-based LLM hallucination. | [SVAREPORT] | related: WER, spoken hallucination; Issue 2, reliability & hallucination control |
| **Shared voice-agent benchmark** | The workshop's identified gap: the absence of a common, cross-vendor evaluation benchmark for voice-agent reliability, as distinct from single-component benchmarks like WER. | [SVAREPORT] | related: Task Success Rate; Issue 2 |
| **Incremental speech processing** | Processing a user's utterance word-by-word or chunk-by-chunk as it arrives, rather than waiting for a complete utterance, to enable lower-latency response planning. | [SVAREPORT] | related: endpointing, barge-in; Issue 3, real-time interaction |
| **Open Floor Protocol** | A multi-agent, multi-human conversational interoperability standard for coordinating turn-taking and floor control across independently built voice agents and human participants sharing the same conversation. | [SVAREPORT]; Open Voice Interoperability Initiative | related: Open Voice Interoperability Initiative (OVON); Issue 4, interoperability scope & architecture |
| **Integration profile (voice interoperability)** | One of four levels at which the workshop found voice-agent interoperability could be standardized — protocol level, API level, dialog-model level, or integration-profile level — with no consensus yet on which level(s) standards work should target. | [SVAREPORT] | related: Open Floor Protocol; Issue 4 |
| **Delegation boundary (voice agent)** | The explicit scope of what actions and data access a user has authorized a voice agent to exercise on their behalf; flagged by the workshop as needing a standard representation rather than per-vendor consent screens. | [SVAREPORT] | related: Know Your Agent (AI-KR CG financial-fraud vocabulary); Issue 5, privacy, trust & delegation boundaries |
| **Identity assertion (voice agent)** | A verifiable claim about who — which person, organization, or agent — is speaking or is being represented by a given voice-agent turn, needed for both trust and dispute-resolution purposes. | [SVAREPORT] | related: delegation boundary; Issue 5 |
| **Auditable agent action** | A voice-agent action (a purchase, a booking, a data disclosure) recorded in a form a user or reviewer can later inspect and verify; identified as a governance gap by the workshop. | [SVAREPORT] | related: delegation boundary, identity assertion; Issue 5 |
| **Multimodal intent fusion** | Combining signals from more than one modality (e.g. speech plus gaze, or speech plus touch) to resolve a single user intent; an unresolved standards area per the workshop. | [SVAREPORT] | related: gaze-aware dialog, time alignment; Issue 6, multimodal coordination & synchronization |
| **Gaze-aware dialog** | A dialog system design that incorporates where a user is looking as an input signal alongside speech, relevant to smart-glasses and immersive voice agents. | [SVAREPORT] | related: multimodal intent fusion; Issue 6 |
| **Time alignment (multimodal)** | Synchronizing timestamps across independently captured modality streams (audio, video, gaze, touch) so a multimodal voice agent can correctly attribute which signals belong to the same moment in the interaction. | [SVAREPORT] | related: multimodal intent fusion, speaker diarization; Issue 6 |
| **Embeddable voice agent (accessibility)** | A voice agent designed to be inserted into third-party or immersive (e.g. WebXR) content specifically to provide an accessible interaction path for blind or low-vision users, rather than as a general-purpose assistant. | [SVAREPORT] | related: Semantic 3D content accessibility; Issue 7, accessibility in immersive/web contexts |
| **Semantic 3D content accessibility** | Metadata and structural conventions that make three-dimensional or immersive web content legible to a voice agent — and thence to the user — in the way ARIA makes 2D DOM content legible to a screen reader. | [SVAREPORT]; W3C Semantic 3D Content Accessibility CG | related: embeddable voice agent, Accessibility conformance (voice); Issue 7 |
| **Persona safety (voice agent)** | Design and governance constraints on a voice agent's adopted persona (name, voice, personality) intended to prevent deceptive impersonation or inappropriate emotional manipulation of the user. | [SVAREPORT] | related: Limited Voice Options; Issue 8, cultural, emotional & persona adaptation |
| **Emotion signaling (voice agent)** | A voice agent's use of prosodic or lexical cues to convey an emotional register (e.g. empathy, urgency); identified by the workshop as an area lacking shared conventions or safety guidance. | [SVAREPORT] | related: prosody, persona safety; Issue 8 |
| **Culturally-aware dialog behavior** | Adapting a voice agent's conversational conventions (directness, formality, turn-taking norms) to the cultural context of the user; flagged as unresolved standards territory by the workshop. | [SVAREPORT] | related: persona safety, turn-taking; Issue 8 |

## Notes and provenance

Category 5 (Commerce & settlement) has fewer terms in this domain than others; voice-specific
commerce vocabulary is comparatively immature and is flagged as an area for further contribution.


Several terms (VoiceInteractionState, VoiceContext,
VoicePlaybackController, VoiceSessionRecovery,
VoiceTask, VoiceTaskQueue, VoiceTaskStatus,
VoiceTaskResult, VoiceTaskCallback) originate as proposed WebIDL
types in the CG's own voiceAI drafts and are carried into this vocabulary as candidate terms
rather than externally sourced definitions; they should be flagged as CG-internal proposals on
submission, not established terms of art.


Appendix A terms are sourced from repository README files current as of this draft and should
be re-checked against the repositories' own glossary/concepts documentation (where one exists)
before formal submission, since framework terminology evolves quickly.


Appendix B terms come from an unpublished manuscript and have no external citation available yet;
treat them as editor-proposed working terminology, not established usage, until the manuscript
is published.


Appendix C terms paraphrase the workshop report's eight cross-cutting issues into individual
vocabulary entries; the report itself frames these as an agenda for near-term Community Group
work rather than settled definitions, and each entry should be checked against the full report
text before formal submission.

## References

- **[FDBENCH]** [Full-Duplex-Bench: A Benchmark to Evaluate Full-duplex Spoken Dialogue Models on Turn-taking Capabilities](https://arxiv.org/abs/2503.04721) (2025)
- **[TAUVOICE]** [τ-Voice: Benchmarking Full-Duplex Voice Agents on Real-World Domains](https://arxiv.org/pdf/2603.13686) (2026)
- **[TURNEOT]** [Thai Semantic End-of-Turn Detection for Real-Time Voice Agents](https://arxiv.org/pdf/2510.04016) (2025)
- **[IHBENCH]** [IHBench: Evaluating Post-Interruption Recovery in Voice Agents with Structured Workflows](https://arxiv.org/pdf/2606.19595) (2026)
- **[ORALVOICE]** [Scalable and Personalized Oral Assessments Using Voice AI](https://arxiv.org/html/2603.18221v1) (2026)
- **[WEB-SPEECH-API]** [Web Speech API](https://wicg.github.io/speech-api/) (WICG)
- **[SSML10]** [Speech Synthesis Markup Language (SSML) Version 1.1](https://www.w3.org/TR/speech-synthesis11/) (W3C)
- **[VOICEXML21]** [Voice Extensible Markup Language (VoiceXML) 2.1](https://www.w3.org/TR/voicexml21/) (W3C)
- **[EMMA20]** [EMMA: Extensible MultiModal Annotation markup language](https://www.w3.org/TR/emma/) (W3C)
- **[MRCPV2]** [Media Resource Control Protocol Version 2 (MRCPv2)](https://www.rfc-editor.org/rfc/rfc6787) (IETF)
- **[WCAG22]** [Web Content Accessibility Guidelines (WCAG) 2.2](https://www.w3.org/TR/WCAG22/) (W3C)
- **[SVAREPORT]** [W3C Workshop on Smart Voice Agents -- Report](https://www.w3.org/news/2026/w3c-workshop-report-smart-voice-agents/) (W3C — 31 March 2026)

## Conformance

This document does not define conformance criteria; it is a terminology collection for review, discussion, and possible future incorporation into a normative CG vocabulary.

---
License: CC BY 4.0.