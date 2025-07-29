  <p>
      Understanding and modeling time-dependent data is crucial in many fields. This document outlines the foundational concepts of time series analysis, starting with the building blocks of random variables and stochastic processes, and progressing to the widely used AR, MA, and ARMA models. These tools allow us to characterize, predict, and analyze data that evolves randomly over time.
    </p>
    <h3><strong>Random Variables and Stochastic Processes</strong></h3>
    <p>
      A <strong>random variable</strong> is a function that assigns a real number to each outcome in a sample space of a random experiment. It's a mathematical representation of a quantity whose value is subject to variations due to chance. Random variables are typically classified as discrete or continuous.
    </p>
    <p>
      A <strong>stochastic process</strong> is a collection of random variables indexed by time, denoted as {X<sub>t</sub> | t ∈ T}. Each random variable X<sub>t</sub> represents the state of a system at time <em>t</em>. Stochastic processes are fundamental for modeling systems that evolve randomly over time.
    </p>
    <h3><strong>Probability Distributions</strong></h3>
    <p>
      A <strong>Probability Density Function (PDF)</strong> describes the likelihood of a continuous random variable taking on a value within a specific range. For a continuous random variable <i>X</i>, the probability that <i>X</i> lies between <i>a</i> and <i>b</i> is the integral of its PDF, f(x), from <i>a</i> to <i>b</i>.
    </p>
    <p>
      The <strong>Gaussian (or Normal) distribution</strong> is a symmetric, bell-shaped curve defined by its mean (μ) and variance (σ²). It is widely used because many natural phenomena approximate this distribution.
    </p>
    <h2>Stationarity in Time Series</h2>
    <p>For a stochastic process to be analyzed with standard models, it often needs to be <strong>stationary</strong>, meaning its statistical properties do not change over time.</p>
    <h3><strong>Strictly Stationary Process</strong></h3>
    <p>
      A time series {X<sub>t</sub>} is <strong>strictly stationary</strong> if its joint probability distribution remains unchanged under shifts in time. That is, for any set of time indices t<sub>1</sub>, ..., t<sub>m</sub> and any time shift τ, the joint distribution of (X<sub>t₁+τ</sub>, ..., X<sub>tₘ+τ</sub>) is the same as that of (X<sub>t₁</sub>, ..., X<sub>tₘ</sub>).
    </p>
    <h3><strong>Wide-Sense Stationary (WSS) Process</strong></h3>
<p>
  A <strong>wide-sense stationary</strong> (WSS) process is a type of stochastic process whose key statistical properties do not change over time. It is also called <strong>covariance stationary</strong>.
</p>
<p>
  For a process {X<sub>t</sub>} to be WSS, it must satisfy the following three conditions:
</p>

<ol>
  <li><strong>Constant Mean:</strong> The expected value stays the same at all times.<br>
    E[X<sub>t</sub>] = μ
  </li>
  <li><strong>Constant Variance:</strong> The variance is constant and finite.<br>
    Var(X<sub>t</sub>) = σ² &lt; ∞
  </li>
  <li><strong>Time-Invariant Covariance:</strong> The covariance between values at two different times depends only on the <em>time difference</em> (lag τ), not the actual time.<br>
    Cov(X<sub>t</sub>, X<sub>t+τ</sub>) = γ(τ)
  </li>
</ol>

<h4><strong>White Noise: A Special Case of WSS</strong></h4>
<p>
  White noise is the simplest example of a WSS process. It is a sequence of random variables {ε<sub>t</sub>} with the following properties:
</p>

<ul>
  <li><strong>Zero Mean:</strong> E[ε<sub>t</sub>] = 0</li>
  <li><strong>Constant Variance:</strong> Var(ε<sub>t</sub>) = σ²</li>
  <li><strong>No Correlation Over Time:</strong> Cov(ε<sub>t</sub>, ε<sub>s</sub>) = 0 for all t ≠ s</li>
</ul>

<p>
  These conditions make white noise not only WSS but also an important building block for more complex models like AR, MA, and ARMA. In fact, the error terms (ε<sub>t</sub>) in those models are usually assumed to be white noise.
</p>
      If the ε<sub>t</sub> values also follow a Gaussian distribution, it is called <strong>Gaussian white noise</strong>. Many time series models describe how this fundamental white noise process is transformed by a system.
    </p>
    <h2>LTI Systems and Their Application to Time Series</h2>
    <p>Linear Time-Invariant (LTI) systems are a primary tool for analyzing and modeling time series. A stationary time series can often be viewed as the output of an LTI system whose input is white noise.</p>    
    <h3><strong>LTI Systems and Convolution</strong></h3>
    <p>
      An <strong>LTI system</strong> is a system that is both <strong>linear</strong> (obeys the superposition principle) and <strong>time-invariant</strong> (its behavior doesn't change over time).
    </p>
    <p>
      The output <i>y(t)</i> of an LTI system is determined by the <strong>convolution</strong> of the input signal <i>x(t)</i> with the system's unique impulse response <i>h(t)</i>. Convolution is a mathematical operation expressed as:
    </p>
    <div>
      y(t) = ∫<sub>-∞</sub><sup>∞</sup> x(τ) h(t - τ) dτ
    </div>    
    <h3><strong>Output of LTI Systems with WSS Inputs</strong></h3>
    <p>When a WSS process, such as a time series, is passed through a stable LTI system:</p>
    <ul>
        <li>The output process is also WSS.</li>
        <li>If the input process is Gaussian, the output process will also be Gaussian. The linear transformation preserves the nature of the distribution.</li>
    </ul>
    <h2>Linear Time Series Models: AR, MA, and ARMA</h2>
    <p>
      The concepts of stationary processes and LTI systems lead to a powerful set of time series models. The <strong>Wold Decomposition Theorem</strong> provides the theoretical justification, stating that any WSS time series can be represented as the sum of a predictable (deterministic) component and a stochastic component. This stochastic part can be modeled as the output of an LTI system fed by white noise, leading to the three main classes of linear models.
    </p>
<h3><strong>Autoregressive (AR) Model</strong></h3>
<p>
  An <strong>AR(p)</strong> model expresses the current value of a time series as a linear combination of its own <i>p</i> previous values, along with a random noise component. In simple terms, it’s like predicting today based on the past few days. This makes it a regression of the series against its own past values.
</p>
<div>
  <strong>Standard Form:</strong><br>
  X<sub>t</sub> = c + φ<sub>1</sub>X<sub>t−1</sub> + φ<sub>2</sub>X<sub>t−2</sub> + ... + φ<sub>p</sub>X<sub>t−p</sub> + ε<sub>t</sub><br>
  <br/>
  where c is a constant term
  <br/>
  φ<sub>1</sub>, ..., φ<sub>p</sub> are model parameters,<br/>
  and ε<sub>t</sub> is a white noise term with zero mean and constant variance
</div>
<br/>
<p>
  Using the <strong>backshift operator</strong> (B), defined by BX<sub>t</sub> = X<sub>t−1</sub>, the model can be expressed more compactly:
</p>
<div>
  <strong>Backshift Notation:</strong><br>
  (1 − φ<sub>1</sub>B − φ<sub>2</sub>B<sup>2</sup> − ... − φ<sub>p</sub>B<sup>p</sup>)X<sub>t</sub> = c + ε<sub>t</sub><br>
  or<br>
  φ(B)X<sub>t</sub> = c + ε<sub>t</sub>
</div>
<p>
<br/>
  For the AR model to be <strong>stationary</strong>, the roots of the characteristic polynomial φ(z) must lie <strong>outside</strong> the unit circle in the complex plane. This ensures the influence of past terms diminishes over time.
</p>
    <h3><strong>Moving Average (MA) Model</strong></h3>
    <p>
      An <strong>MA(q)</strong> model describes the current value of the series as a linear combination of the current and <i>q</i> previous white noise error terms. It models short-run shocks whose effects disappear after <i>q</i> periods.
    </p>
    <div>
      <strong>Standard Form:</strong><br>
      X<sub>t</sub> = μ + ε<sub>t</sub> + θ<sub>1</sub>ε<sub>t−1</sub> + θ<sub>2</sub>ε<sub>t−2</sub> + ... + θ<sub>q</sub>ε<sub>t−q</sub><br/>
      <br/>
        where μ = mean of the series (a constant)<br>
        ε<sub>t</sub> = current white noise (random error)<br>
        θ<sub>1</sub>, θ<sub>2</sub>, ..., θ<sub>q</sub> = weights on past errors<br>
  and ε<sub>t</sub> is a white noise term with zero mean and constant variance
    </div>
    <br/>
    <p>
      Using the backshift operator on the error terms:
    </p>
    <div>
      <strong>Backshift Notation:</strong><br>
      X<sub>t</sub> = μ + (1 + θ<sub>1</sub>B + θ<sub>2</sub>B<sup>2</sup> + ... + θ<sub>q</sub>B<sup>q</sup>)ε<sub>t</sub><br>
      or<br>
      X<sub>t</sub> = μ + θ(B)ε<sub>t</sub>
    </div>
    <br/>
    <p>MA models are always stationary.</p>
    <h3><strong>Autoregressive Moving Average (ARMA) Model</strong></h3>
    <p>
      An <strong>ARMA(p, q)</strong> model combines both AR and MA components. It describes the current value of the series based on <i>p</i> previous values of the series and <i>q</i> previous error terms. This provides a more parsimonious (simpler) model for complex time series patterns.
    </p>
    <div>
      <strong>Standard Form:</strong><br>
      X<sub>t</sub> = c + φ<sub>1</sub>X<sub>t−1</sub> + ... + φ<sub>p</sub>X<sub>t−p</sub> + ε<sub>t</sub> + θ<sub>1</sub>ε<sub>t−1</sub> + ... + θ<sub>q</sub>ε<sub>t−q</sub>
    </div>
    <p>
      In backshift notation, the model elegantly combines the AR and MA polynomials:
    </p>
    <div>
      <strong>Backshift Notation:</strong><br>
      φ(B)X<sub>t</sub> = c + θ(B)ε<sub>t</sub>
    </div>
    <p>Stationarity of an ARMA model depends entirely on its AR component.</p>
    <h2>Applications</h2>
    <p>
      AR, MA, and ARMA models are widely used for modeling and forecasting time series in numerous domains, including:
    </p>
    <ul>
      <li>Economics and finance (e.g., stock prices, inflation)</li>
      <li>Weather and climate prediction</li>
      <li>Signal processing and control systems</li>
      <li>Retail and business sales forecasting</li>
      <li>Healthcare analytics and environmental monitoring</li>
    </ul>
    <p>
      These models are supported by a rich body of linear system theory and form the basis for many advanced time series methods.
    </p>
