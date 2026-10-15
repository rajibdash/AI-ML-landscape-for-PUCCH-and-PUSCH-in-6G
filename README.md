# AI/ML landscape for PUCCH and PUSCH in 6G

Investigation and research into evolving the AI/ML landscape for uplink channels
in 6G, with a focus on the Physical Uplink Control Channel (PUCCH) and
Physical Uplink Shared Channel (PUSCH) from a Radio Access Network (RAN)
optimization perspective. The ideas below are research directions, with
deployment subject to latency budgets, model complexity, interoperability, and
the tradeoff between performance gains and operational cost.

## PUCCH

- **Intelligent HARQ optimization:** Use Layer 2 machine-learning models to
  predict block error rates (BLER) and likely ACK/NACK outcomes from channel,
  mobility, and link-adaptation context. Explore adapting retransmission timing,
  redundancy versions, and PUCCH resource selection while preserving robust
  ACK/NACK detection.
  - **Rationale:** HARQ feedback reliability and timing directly affect
    retransmission latency, radio-resource use, and the scheduler's view of link
    quality. Better prediction may reduce unnecessary feedback or retransmits,
    but must not increase missed ACK/NACKs or consume capacity needed by other
    uplink control information.
- **Spatial-temporal beam prediction and tracking:** Use recurrent neural
  networks (RNNs) or Transformers to forecast beam changes from historical
  trajectories, mobility, and available reference-signal measurements. Study
  joint beam prediction and tracking across UE and gNodeB beams, including
  when to refresh measurements or trigger beam switching.
  - **Rationale:** Timely beam alignment can improve uplink reliability and
    spectral efficiency, especially at high frequencies and under mobility.
    Prediction may reduce frequent sounding and feedback overhead, but stale
    predictions can cause beam misalignment; measurement cadence must fit RAN
    latency and control-capacity constraints.
- **AI-driven CSI compression and feedback:** Use generative models or
  autoencoders at the UE to compress multi-antenna channel state information
  (CSI), then reconstruct it at the gNodeB for beam management, link adaptation,
  or scheduling. Evaluate feedback quantization and reconstruction error under
  changing channels; exact reconstruction is not guaranteed.
  - **Rationale:** CSI feedback can consume substantial PUCCH resources as
    antenna and beam dimensions grow. Compression can free uplink control
    capacity and support faster RAN decisions, provided the residual error does
    not undermine beam selection, scheduling, or link reliability, and both
    ends can support interoperable model behavior.
- **Reference-signal and pathloss prediction across resources:** Predict
  pathloss or reference-signal measurements for one set of uplink resources
  using measurements from another. Inputs and predictions can span different
  spatial locations, times, frequencies, and transmission/reception points
  (TRPs), including measurements of the same or different reference-signal
  types; investigate using these predictions to guide measurement and resource
  selection.
  - **Rationale:** More timely pathloss estimates can inform uplink power
    control, beam management, and resource selection without requiring
    measurement of every resource. Prediction error can cause excess UE power,
    interference, or unreliable links, so measurement savings must be balanced
    against those RAN-wide effects.

## PUSCH

- **Neural channel estimation and tracking:** Replace or augment traditional
  linear minimum mean squared error (LMMSE) estimators with deep neural
  networks (DNNs) to track rapid channel changes, including in complex
  non-line-of-sight (NLOS), high-mobility, and multi-antenna scenarios using
  available reference signals. Cell-edge throughput improvements (including a
  proposed target of over 30%) should be validated against representative
  baselines, channel conditions, and implementation complexity.
  - **Rationale:** More accurate channel estimates can improve PUSCH
    demodulation, coverage, and spectral efficiency, allowing the RAN scheduler
    to make better link-adaptation decisions. Gains must be achieved within
    receiver processing and scheduling latency budgets and without excessive
    compute or energy cost.
- **End-to-end neural receivers:** Replace the cascaded physical-layer chain
  of channel estimation, equalization, demapping, and decoding with a unified
  multi-layer neural receiver, and evaluate its reliability, complexity,
  generalization, and compatibility with existing RAN interfaces and operating
  conditions.
  - **Rationale:** Joint optimization may exploit dependencies across receiver
    stages to improve reliability or reduce processing delay. However, the
    receiver must meet stringent PUSCH latency and error-rate targets, and
    model complexity, maintainability, and interoperability can constrain
    deployment.
- **Energy-efficient neural demappers:** Explore spiking neural networks
  (SNNs) for low-complexity, scalable demapping, particularly for
  high-order constellations. Compare implementation cost, processing latency,
  and energy use alongside error performance over representative channel and
  modulation conditions.
  - **Rationale:** Demapping cost can grow with modulation order and receiver
    workload. Lower-power processing could improve UE battery life and RAN
    energy efficiency, but only if complexity savings do not compromise
    throughput, reliability, or real-time decoding deadlines.
- **Joint AMC and power-control optimization:** Apply deep reinforcement
  learning (DRL) to jointly select adaptive modulation and coding (AMC) and
  uplink transmit power in coordination with scheduling and channel conditions.
  Optimize data rate while accounting for interference, network energy
  efficiency, and UE battery life.
  - **Rationale:** AMC and power control jointly determine uplink throughput,
    coverage, interference, and retransmission risk. Coordinated decisions can
    improve spectral and energy efficiency, but must respect power limits,
    scheduler timing, and reliability targets across users rather than
    optimizing an individual link in isolation.
- **Semantic and task-oriented waveform design:** Use deep-learning
  autoencoders to learn compact semantic representations and jointly optimize
  waveforms and constellations for target tasks, including Sub-THz bands and
  extreme-data-rate services. Assess performance against conventional
  bit-oriented links and relevant channel, coding, and receiver constraints.
  - **Rationale:** Transmitting task-relevant information rather than all
    source bits may reduce airtime, latency, and energy for suitable services.
    The benefit depends on application tolerance to information loss and on
    practical waveform, receiver, and interoperability constraints in the RAN.

## References
1. https://www.sharetechnote.com/html/6G/6G_TDoc_AI_ML.html
