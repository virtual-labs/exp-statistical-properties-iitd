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
      An <strong>Autoregressive (AR) model</strong> is a statistical model used in time series analysis where the current value of a series is predicted based on a linear combination of its own past values. It is denoted as <strong>AR(p)</strong>, where 'p' represents the order, indicating the number of preceding values used in the prediction. The core idea is that the future is dependent on the past.
    </p>
    <div>
      <strong>Standard Form:</strong><br>
      The mathematical representation of an AR(p) model is:<br><br>
      X<sub>t</sub> = c + φ<sub>1</sub>X<sub>t−1</sub> + φ<sub>2</sub>X<sub>t−2</sub> + ... + φ<sub>p</sub>X<sub>t−p</sub> + ε<sub>t</sub>
      <br/><br/>
      where:
      <ul>
        <li><strong>X<sub>t</sub></strong> is the value of the time series at time <i>t</i>.</li>
        <li><strong>c</strong> is a constant term.</li>
        <li><strong>φ<sub>1</sub>, ..., φ<sub>p</sub></strong> are the model parameters that are learned from the data.</li>
        <li><strong>p</strong> is the order of the model, representing the number of lag terms.</li>
        <li><strong>ε<sub>t</sub></strong> is the white noise error term, which accounts for randomness not captured by the model.</li>
      </ul>
    </div>
    <br/>
    <p>
      An AR model is conceptually similar to a linear regression where the variable is regressed against its own past values. For the model to be stationary, meaning its statistical properties do not change over time, there are constraints on the model's parameters.
    </p>   
    <h3><strong>Moving Average (MA) Model</strong></h3>
    <p>
      A <strong>Moving Average (MA) model</strong> describes the current value of a time series as a linear combination of the current and past white noise error terms. It is denoted as <strong>MA(q)</strong>, where 'q' is the order and indicates how many past error terms are included. This model is useful for capturing short-run shocks where the effects dissipate after 'q' periods. Unlike AR models, finite MA models are always stationary.
    </p>  
    <div>
      <strong>Standard Form:</strong><br>
      The MA(q) model is expressed as:<br><br>
      X<sub>t</sub> = μ + ε<sub>t</sub> + θ<sub>1</sub>ε<sub>t−1</sub> + θ<sub>2</sub>ε<sub>t−2</sub> + ... + θ<sub>q</sub>ε<sub>t−q</sub>
      <br/><br/>
      where:
      <ul>
        <li><strong>X<sub>t</sub></strong> is the value of the time series at time <i>t</i>.</li>
        <li><strong>μ</strong> is the mean of the series.</li>
        <li><strong>ε<sub>t</sub></strong> is the current white noise error term.</li>
        <li><strong>θ<sub>1</sub>, ..., θ<sub>q</sub></strong> are the weights applied to the past error terms.</li>
        <li><strong>q</strong> is the order of the model.</li>
      </ul>
    </div>
    <br/>
    <p>
      The MA model is essentially a finite impulse response (FIR) filter applied to white noise.
    </p>  
    <h3><strong>Autoregressive Moving Average (ARMA) Model</strong></h3>
    <p>
      An <strong>Autoregressive Moving Average (ARMA) model</strong> combines both AR and MA components to describe a stationary time series. It models the current value as a function of both past values of the series and past error terms. An <strong>ARMA(p,q)</strong> model has an autoregressive part of order 'p' and a moving average part of order 'q'. This combination allows for a more parsimonious representation of a time series compared to a pure AR or MA model.
    </p>   
    <div>
      <strong>Standard Form:</strong><br>
      The equation for an ARMA(p, q) model is:<br><br>
      X<sub>t</sub> = c + φ<sub>1</sub>X<sub>t−1</sub> + ... + φ<sub>p</sub>X<sub>t−p</sub> + ε<sub>t</sub> + θ<sub>1</sub>ε<sub>t−1</sub> + ... + θ<sub>q</sub>ε<sub>t−q</sub>
      <br/><br/>
      where:
      <ul>
        <li><strong>X<sub>t</sub></strong> is the value of the time series at time t.</li>
        <li><strong>c</strong> is a constant.</li>
        <li><strong>φ<sub>i</sub></strong> are the autoregressive parameters.</li>
        <li><strong>θ<sub>j</sub></strong> are the moving average parameters.</li>
        <li><strong>ε<sub>t</sub></strong> is the white noise error term.</li>
      </ul>
    </div>    
    <h2><strong>Z-Transform Analysis of Time Series Models</strong></h2>
    <p>
      The z-transform is a mathematical tool that converts a discrete-time signal (like a time series) into a complex frequency-domain representation. It is the discrete-time equivalent of the Laplace transform and is instrumental in analyzing the properties of time series models.
    </p>    
    <h3><strong>Z-Transform Representation</strong></h3>
    <p>
      Using the backshift operator <i>B</i>, where <i>B</i>X<sub>t</sub> = X<sub>t-1</sub>, the ARMA(p,q) model can be written in polynomial form:
    </p>
    <div>
      (1 - φ<sub>1</sub>B - ... - φ<sub>p</sub>B<sup>p</sup>)X<sub>t</sub> = c + (1 + θ<sub>1</sub>B + ... + θ<sub>q</sub>B<sup>q</sup>)ε<sub>t</sub>
    </div>
    <br>
    <p>
      Let Φ(B) and Θ(B) be the polynomials in the backshift operator. Replacing <i>B</i> with z<sup>-1</sup> gives the z-transform representation:
    </p>
    <div>
      Φ(z<sup>-1</sup>)X(z) = c' + Θ(z<sup>-1</sup>)E(z)
    </div>
    <br>
    <p>
      where <i>X(z)</i> and <i>E(z)</i> are the z-transforms of the time series and the error term, respectively.
    </p>   
    <h3><strong>Transfer Function</strong></h3>
    <p>
      The transfer function, H(z), of an ARMA model describes the relationship between the input (error term) and the output (time series) in the z-domain. It is defined as the ratio of the MA polynomial to the AR polynomial:
    </p>
    <div>
      <strong>H(z) = X(z) / E(z) = Θ(z<sup>-1</sup>) / Φ(z<sup>-1</sup>)</strong>
    </div>
    <br>
    <ul>
        <li>For a pure <strong>AR(p)</strong> model, the transfer function is H(z) = 1 / Φ(z<sup>-1</sup>), which is an all-pole function.</li>
        <li>For a pure <strong>MA(q)</strong> model, the transfer function is H(z) = Θ(z<sup>-1</sup>), which is an all-zero function.</li>
        <li>An <strong>ARMA(p,q)</strong> model has a pole-zero transfer function.</li>
    </ul>
    <h3><strong>Stability and Invertibility Conditions</strong></h3>
    <p>
      The stability of an ARMA model is determined by the roots of the autoregressive polynomial, Φ(z). For a model to be stable (and thus stationary), all the roots of Φ(z) must lie outside the unit circle in the z-plane. This is equivalent to the poles of the transfer function H(z) lying inside the unit circle when expressed in terms of z.
    </p>
    <p>
      The invertibility of an ARMA model is determined by the roots of the moving average polynomial, Θ(z). For the model to be invertible, all the roots of Θ(z) must lie outside the unit circle. Invertibility ensures that the model can be represented as a pure autoregressive process of infinite order.
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

