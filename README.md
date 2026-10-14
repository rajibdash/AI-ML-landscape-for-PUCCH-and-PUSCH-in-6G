# AI/ML landscape for PUCCH and PUSCH in 6G

Investigation and research into evolving the AI/ML landscape for uplink channels
in 6G, with a focus on the Physical Uplink Control Channel (PUCCH) and
Physical Uplink Shared Channel (PUSCH).

## PUCCH

- **Intelligent HARQ optimization:** Use Layer 2 machine-learning models to
  predict block error rates (BLER) dynamically and optimize retransmission
  timing, redundancy versions, and resource allocation. The goal is to reduce
  control overhead on PUCCH while meeting reliability and latency targets.
- **Spatial-temporal beam prediction and tracking:** Use recurrent neural
  networks (RNNs) or Transformers to forecast beam movement from historical
  trajectories. Proactive beam switching could reduce reliance on continuous,
  resource-intensive uplink sounding reference signal (SRS) transmissions.
- **AI-driven CSI compression and feedback:** Use generative models or
  autoencoders at the UE to compress multi-antenna channel state information
  (CSI), then reconstruct it at the gNodeB. Evaluate reconstruction fidelity
  against the feedback-overhead reduction; exact reconstruction is not
  guaranteed.
- **Pathloss prediction across resources:** Predict pathloss for one set of
  uplink reference signals using measurements from another set. Inputs and
  predictions can span different spatial locations, times, frequencies, and
  transmission/reception points (TRPs), including measurements of the same or
  different reference-signal types.

## PUSCH

- **Neural channel estimation and tracking:** Replace or augment traditional
  linear minimum mean squared error (LMMSE) estimators with deep neural
  networks (DNNs) to track rapid channel changes, including in complex
  non-line-of-sight (NLOS) and high-mobility scenarios. Cell-edge throughput
  improvements (including a proposed target of over 30%) should be validated
  against representative baselines and channel conditions.
- **End-to-end neural receivers:** Replace the cascaded physical-layer chain
  of channel estimation, equalization, demapping, and decoding with a unified
  multi-layer neural receiver, and evaluate its reliability, complexity, and
  generalization.
- **Energy-efficient neural demappers:** Explore spiking neural networks
  (SNNs) for low-complexity, scalable demapping, particularly for
  high-order constellations, and measure energy use alongside error
  performance.
- **Joint AMC and power-control optimization:** Apply deep reinforcement
  learning (DRL) to jointly select adaptive modulation and coding (AMC) and
  uplink transmit power. Optimize data rate while accounting for network
  energy efficiency and UE battery life.
- **Semantic and task-oriented waveform design:** Use deep-learning
  autoencoders to learn compact semantic representations and jointly optimize
  waveforms and constellations for target tasks, including Sub-THz bands and
  extreme-data-rate services.
