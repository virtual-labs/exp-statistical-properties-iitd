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
  where c is a constant term,<br/>
  φ<sub>1</sub>, ..., φ<sub>p</sub> are model parameters,<br/>
  and ε<sub>t</sub> is a white noise term with zero mean and constant variance.
</div>
<br/>
<p>
  Using the <strong>z-transform operator</strong> (z<sup>−1</sup>), defined by z<sup>−1</sup>X<sub>t</sub> = X<sub>t−1</sub>, the model can be expressed more compactly:
</p>
<div>
  <strong>Z-Transform Representation:</strong><br>
  Taking the z-transform of both sides of the AR(p) model:<br><br>
  X<sub>t</sub> = c + φ<sub>1</sub>X<sub>t−1</sub> + φ<sub>2</sub>X<sub>t−2</sub> + ... + φ<sub>p</sub>X<sub>t−p</sub> + ε<sub>t</sub><br><br>

  Applying the z-transform:<br>
  X(z) = c·1/(1−z<sup>−1</sup>) + φ<sub>1</sub>z<sup>−1</sup>X(z) + φ<sub>2</sub>z<sup>−2</sup>X(z) + ... + φ<sub>p</sub>z<sup>−p</sup>X(z) + ε(z)
</div>
<br>
<div>
  <strong>Solving for X(z):</strong><br>
  Move all X(z) terms to one side:<br>
  [1 − φ<sub>1</sub>z<sup>−1</sup> − φ<sub>2</sub>z<sup>−2</sup> − ... − φ<sub>p</sub>z<sup>−p</sup>]·X(z) = c·1/(1−z<sup>−1</sup>) + ε(z)
</div>
<br>
<div>
  <strong>Transfer Function H(z):</strong><br>
  Define the transfer function from ε(z) to X(z) as:<br>
  H(z) = X(z) / ε(z) = 1 / φ(z)<br>
  where:<br>
  φ(z) = 1 − φ<sub>1</sub>z<sup>−1</sup> − φ<sub>2</sub>z<sup>−2</sup> − ... − φ<sub>p</sub>z<sup>−p</sup><br><br>
  If c ≠ 0, then:<br>
  X(z) = H(z)·ε(z) + c / [(1 − z<sup>−1</sup>)·φ(z)]
</div>

<br/>
<p>
  <strong>Continuous-Time Analogy:</strong> In continuous-time systems, similar dynamics are described using differential equations. For example, a first-order system is modeled as:<br>
  <i>d</i>y(t)/<i>d</i>t + a·y(t) = b·x(t)<br>
  This acts as the continuous-time counterpart of an AR(1) model. Applying the Laplace Transform (continuous analog of the z-transform) gives the transfer function:<br>
  H(s) = Y(s)/X(s) = b / (s + a)<br>
  This shows how autoregressive behavior also exists in continuous systems, though expressed through derivatives and Laplace transforms instead of time shifts and z-transforms.
</p>
<p>
  <strong>Stability Condition:</strong><br>
  The stability of an AR model depends on the location of the poles of the AR polynomial <i>Φ(z)</i>. The system is <em>stable</em> if all roots of Φ(z) lie <strong>inside the unit circle</strong> in the z-domain, i.e.,<br>
  <strong>|z| &lt; 1</strong> for all roots of Φ(z).<br>
  In continuous-time systems, this corresponds to all poles of H(s) lying in the <strong>left-half s-plane</strong> (Re(s) &lt; 0).
</p>

<h3><strong>Moving Average (MA) Model</strong></h3>
<p>
  An <strong>MA(q)</strong> model describes the current value of the series as a linear combination of the current and <i>q</i> previous white noise error terms. It models short-run shocks whose effects disappear after <i>q</i> periods.
</p>
<div>
  <strong>Standard Form:</strong><br>
  X<sub>t</sub> = μ + ε<sub>t</sub> + θ<sub>1</sub>ε<sub>t−1</sub> + θ<sub>2</sub>ε<sub>t−2</sub> + ... + θ<sub>q</sub>ε<sub>t−q</sub><br/>
  <br/>
  where:<br/>
  μ is the mean of the series (a constant),<br/>
  ε<sub>t</sub> is current white noise (zero-mean random error),<br/>
  and θ<sub>1</sub>, ..., θ<sub>q</sub> are weights on past errors.
</div>
<br/>
<p>
  Using the <strong>z-transform operator</strong> (z<sup>−1</sup>), defined as z<sup>−1</sup>ε<sub>t</sub> = ε<sub>t−1</sub>, we can express the model compactly:
</p>
<div>
  <strong>Z-Transform Notation:</strong><br>
  X<sub>t</sub> = μ + (1 + θ<sub>1</sub>z<sup>−1</sup> + θ<sub>2</sub>z<sup>−2</sup> + ... + θ<sub>q</sub>z<sup>−q</sup>)ε<sub>t</sub><br>
  or<br>
  X<sub>t</sub> = μ + θ(z<sup>−1</sup>)ε<sub>t</sub>
</div>
<br/>
<div>
  <strong>Z-Domain Expression:</strong><br>
  Taking the z-transform of both sides gives:<br>
  X(z) = μ·1/(1 − z<sup>−1</sup>) + θ(z<sup>−1</sup>)·ε(z)<br><br>
  where:<br>
  θ(z<sup>−1</sup>) = 1 + θ<sub>1</sub>z<sup>−1</sup> + θ<sub>2</sub>z<sup>−2</sup> + ... + θ<sub>q</sub>z<sup>−q</sup>
</div>
<br/>
<div>
  <strong>Transfer Function H(z):</strong><br>
  The transfer function from ε(z) to X(z) is:<br>
  H(z) = X(z) / ε(z) = θ(z<sup>−1</sup>)<br><br>
  If μ ≠ 0, the full expression becomes:<br>
  X(z) = H(z)·ε(z) + μ / (1 − z<sup>−1</sup>)
</div>
<br/>
<p>
  <strong>Continuous-Time Analogy:</strong> Though less common, a continuous-time analogue to MA behavior could be a system with a finite impulse response to white noise input, such as:<br>
  y(t) = ∫<sub>t−T</sub><sup>t</sup> h(τ)·ε(t−τ) dτ<br>
  where h(τ) is a short-lived kernel and ε(t) is white noise. Unlike AR systems, these don't involve derivatives, just finite-length convolutions.
</p>
<p>
  <strong>Stability Condition:</strong><br>
  The MA model is always <em>stable</em> because it does not involve feedback (no poles except at the origin in the z-domain).<br>
  However, for <em>invertibility</em>, the roots of the MA polynomial <i>Θ(z)</i> must lie <strong>outside the unit circle</strong>, i.e.,<br>
  <strong>|z| &gt; 1</strong> for all roots of Θ(z).<br>
</p>

<h3><strong>Autoregressive Moving Average (ARMA) Model</strong></h3>

<p>
  An <strong>ARMA(p, q)</strong> model combines both autoregressive (AR) and moving average (MA) components. It models the current value of a discrete-time process as a combination of <i>p</i> past values of the process and <i>q</i> past white noise/error terms.
</p>

<div>
  <strong>Standard Form:</strong><br>
  X<sub>t</sub> = μ + φ<sub>1</sub>X<sub>t−1</sub> + ⋯ + φ<sub>p</sub>X<sub>t−p</sub> + ε<sub>t</sub> + θ<sub>1</sub>ε<sub>t−1</sub> + ⋯ + θ<sub>q</sub>ε<sub>t−q</sub>
</div>

<p>
  Using the Z-transform (where the shift operator <i>z<sup>−1</sup></i> represents one time-step delay), the model is written in polynomial form:
</p>

<div>
  <strong>Z-Transform Representation:</strong><br>
  Φ(z)X(z) = Θ(z)E(z) + C(z)
</div>

<p>
  where:<br>
  Φ(z) = 1 − φ<sub>1</sub>z<sup>−1</sup> − φ<sub>2</sub>z<sup>−2</sup> − ⋯ − φ<sub>p</sub>z<sup>−p</sup><br>
  Θ(z) = 1 + θ<sub>1</sub>z<sup>−1</sup> + θ<sub>2</sub>z<sup>−2</sup> + ⋯ + θ<sub>q</sub>z<sup>−q</sup><br>
  E(z): Z-transform of white noise ε<sub>t</sub><br>
  X(z): Z-transform of output signal X<sub>t</sub><br>
  C(z): Z-transform of constant term μ (usually becomes μ/(1−φ<sub>1</sub>−⋯))
</p>

<p>
  <strong>Transfer Function:</strong><br>
  The frequency-domain representation (transfer function) becomes:<br>
  H(z) = Θ(z) / Φ(z)
</p>

<hr>

<h4><strong>Continuous-Time Analogy</strong></h4>
<p>
  In continuous-time systems, dynamics are governed by differential equations. An analogy to the ARMA model would be a linear time-invariant (LTI) system described by:
</p>

<div>
  <i>d<sup>p</sup>y(t)/dt<sup>p</sup> + a<sub>1</sub>d<sup>p−1</sup>y(t)/dt<sup>p−1</sup> + ⋯ + a<sub>p</sub>y(t) = b<sub>0</sub>x(t) + b<sub>1</sub>dx(t)/dt + ⋯ + b<sub>q</sub>d<sup>q</sup>x(t)/dt<sup>q</sup></i>
</div>

<p>
  Taking the Laplace Transform gives the transfer function:<br>
  H(s) = Y(s)/X(s) = (b<sub>0</sub> + b<sub>1</sub>s + ⋯ + b<sub>q</sub>s<sup>q</sup>) / (s<sup>p</sup> + a<sub>1</sub>s<sup>p−1</sup> + ⋯ + a<sub>p</sub>)
</p>

<p>
  Thus, just as the ARMA model uses the ratio of polynomials in <i>z</i>, the continuous-time system uses the ratio of polynomials in <i>s</i>.
</p>
<p>
  <strong>Stability Condition:</strong><br>
  The stability of an ARMA system depends on its AR component. In the z-domain, the system is <em>stable</em> if all poles of the transfer function (roots of Φ(z)) lie inside the unit circle |z| &lt; 1.<br>
  Similarly, in continuous time, the system is stable if all poles of H(s) (roots of the denominator) lie in the left half of the s-plane (Re(s) &lt; 0).
</p>
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
