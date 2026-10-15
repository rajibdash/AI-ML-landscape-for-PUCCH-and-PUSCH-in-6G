# AI/ML landscape for PUCCH and PUSCH in 6G

Investigation and research into evolving the AI/ML landscape for uplink channels
in 6G, with a focus on the Physical Uplink Control Channel (PUCCH) and
Physical Uplink Shared Channel (PUSCH) from a Radio Access Network (RAN)
perspective.

The emphasis here is on how intelligent control loops can improve scheduling,
link adaptation, beam management, uplink reliability, spectral efficiency,
and energy efficiency while respecting 3GPP-oriented constraints such as
latency budgets, reference-signal overhead, control-channel capacity,
implementation complexity, and interoperability with existing PHY/MAC/RRC
procedures.

## PUCCH

- **Intelligent HARQ optimization:** Use Layer 2 machine-learning models to
  predict block error rates (BLER), ACK/NACK reliability, and retransmission
  outcomes from RAN-side observations such as CSI quality, HARQ process
  history, scheduling context, buffer status, and mobility state. The model can
  adapt retransmission timing, redundancy versions, HARQ process prioritization,
  and PUCCH resource selection to reduce control overhead while preserving
  latency and reliability targets.
  - **Rationale:** In 6G uplink, PUCCH must carry increasingly dense control
    signaling with strict latency constraints. Predictive HARQ control can
    reduce unnecessary retransmissions, avoid over-provisioning of control
    resources, and improve edge-user performance when channel conditions change
    faster than static link-adaptation rules can react.

- **Spatial-temporal beam prediction and tracking:** Use recurrent neural
  networks (RNNs), Transformers, or temporal graph models to forecast beam
  evolution from historical beam measurements, gNB measurements, UE mobility
  indicators, SRS/CSI-RS statistics, and beam failure recovery events. This can
  support proactive beam switching, PUCCH resource re-selection, and faster
  beam recovery without relying only on continuous high-rate uplink sounding.
  - **Rationale:** Beam misalignment directly harms uplink control reliability,
    especially for high-frequency 6G deployments and mobility scenarios. Better
    beam prediction reduces control outages, limits unnecessary sounding
    overhead, and helps the RAN maintain robust uplink control quality with less
    signaling.

- **AI-driven CSI compression and feedback:** Use autoencoders, vector
  quantization, or lightweight generative models at the UE to compress uplink
  CSI-related features before feedback, then reconstruct or approximate them at
  the gNodeB for scheduling, precoding, and link adaptation. The optimization
  target is to minimize feedback bits while preserving the accuracy needed for
  beam selection, rank adaptation, and MCS decisions.
  - **Rationale:** PUCCH and related uplink control resources are limited, and
    CSI feedback can become expensive in dense antenna and wideband settings.
    Learned compression can reduce feedback overhead, improve scalability for
    massive MIMO and multi-TRP deployments, and preserve enough channel detail
    for RAN decisions without requiring exact reconstruction.

- **Pathloss prediction across resources:** Predict pathloss for one set of
  uplink reference signals using measurements from another set, including across
  different times, spatial locations, frequencies, beams, and transmission /
  reception points (TRPs). Inputs may include UE measurements, historical SRS
  statistics, neighboring-cell observations, and mobility context.
  - **Rationale:** Accurate pathloss prediction helps the RAN allocate PUCCH
    resources more intelligently, tune power control, and reduce the amount of
    probing needed to maintain reliable uplink control. This is especially
    useful when reference-signal budgets are constrained or when the network
    must infer channel quality across heterogeneous TRPs and carrier layers.

## PUSCH

- **Neural channel estimation and tracking:** Replace or augment traditional
  linear minimum mean squared error (LMMSE) estimators with deep neural
  networks (DNNs) or hybrid model-based/data-driven estimators to track rapid
  channel changes in non-line-of-sight (NLOS), high-mobility, and frequency-
  selective scenarios. The RAN should evaluate improvements in throughput,
  BLER, and MCS stability against representative baselines and channel models.
  - **Rationale:** PUSCH performance depends strongly on channel-estimation
    accuracy, especially at the cell edge or under fast fading. Neural
    estimators can exploit nonlinear structure and temporal correlation more
    effectively than fixed linear estimators, potentially improving robustness
    when classical assumptions break down.

- **End-to-end neural receivers:** Replace the cascaded physical-layer chain of
  channel estimation, equalization, demapping, and decoding with a unified
  multi-layer neural receiver, or a hybrid receiver that keeps selected
  analytical blocks and learns the remaining impairments. Evaluate reliability,
  computational load, latency, explainability, and generalization across
  numerologies and channel conditions.
  - **Rationale:** In 6G, uplink receivers may need to adapt to more diverse
    waveforms, bandwidths, and propagation conditions than traditional receiver
    chains were designed for. End-to-end learning can potentially capture joint
    impairments and improve detection performance, but only if the RAN can meet
    strict processing budgets and maintain stable behavior across deployments.

- **Energy-efficient neural demappers:** Explore spiking neural networks (SNNs)
  or other low-power inference models for demapping, especially for high-order
  constellations and massive uplink throughput. Measure energy consumption,
  inference latency, and error-rate performance under realistic accelerator or
  CPU/GPU constraints.
  - **Rationale:** Demapping is a repeated, high-throughput operation in the
    uplink receiver chain. Energy-efficient inference is important for scalable
    base-station deployment, and low-power models can help the RAN balance
    throughput gains with operational cost and thermal limits.

- **Joint AMC and power-control optimization:** Apply deep reinforcement
  learning (DRL) or constrained optimization to jointly select adaptive
  modulation and coding (AMC), uplink transmit power, and possibly HARQ-aware
  link adaptation parameters. Optimize throughput, BLER, fairness, and UE power
  consumption while respecting interference and regulatory constraints.
  - **Rationale:** AMC and power control are tightly coupled in the uplink.
    Coordinated decisions can improve spectral efficiency and reduce battery
    drain, but only if the controller learns to handle feedback delay, mobility,
    and inter-cell interference in a stable and policy-compliant way.

- **Semantic and task-oriented waveform design:** Use deep-learning autoencoders
  to learn compact semantic representations and jointly optimize waveforms,
  constellations, and coding for target tasks, including Sub-THz bands,
  sensing-assisted communication, and extreme-data-rate services. Consider
  task-aware metrics rather than only bit-level reconstruction quality.
  - **Rationale:** Future 6G RANs may need to optimize not just bit delivery but
    also task success, latency, and context delivery. Semantic waveform design
    can reduce unnecessary payload overhead and improve robustness in challenging
    propagation conditions, but it must still coexist with standardized uplink
    procedures and receiver interoperability.

## References
1. https://www.sharetechnote.com/html/6G/6G_TDoc_AI_ML.html
