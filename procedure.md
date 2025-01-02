<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <link href="https://cdn.jsdelivr.net/npm/tailwindcss@2.2.19/dist/tailwind.min.css" rel="stylesheet">
</head>
<body>
    <ul>
        <li>
            <strong>Input Parameters:</strong>
            <ul>
                <li><strong>Number of Samples:</strong> Use the input field to enter the number of samples, which refers to the total count of discrete data points that represent the signal over a certain time period.</li>
                <li><strong>Channel Impulse Response:</strong> Enter the impulse response values or coefficients that describe the effect of the channel on the transmitted signal.</li>
                <li><strong>AR Coefficients:</strong> Specify the coefficients for the Auto-Regressive (AR) part of the ARMA model, which defines how past values of the signal influence the current value.</li>
                <li><strong>MA Coefficients:</strong> Specify the coefficients for the Moving Average (MA) part of the ARMA model, which defines how past noise terms influence the current value of the signal.</li>
            </ul>
        </li>
        <li>
            <strong>Generate the WSS Signal:</strong> 
            Click the <em>“Generate WSS”</em> button to create a WSS signal has statistical properties (like mean and autocorrelation) that do not change with time shifts.
        </li>
        <li>
            <strong>Generate the Channel Impulse Response:</strong> 
            Click the <em>“Generate CIR”</em> button to generate the impulse response values or coefficients.
        </li>
        <li>
            <strong>Generate Output Signal when System is LTI:</strong> 
            Click the <em>“Generate Output”</em> button to perform the convolution of the input WSS signal with the LTI channel coefficients. The resulting signal is the output.
        </li>
        <li>
            <strong>Check Auto-correlation for the Input Signal:</strong> 
            Click the <em>“Check Auto-correlation for Input”</em> button to measure the similarity between the input WSS signal and a time-shifted version of itself.
        </li>
        <li>
            <strong>Check Auto-correlation for the Output Signal:</strong> 
            Click the <em>“Check Auto-correlation for Output”</em> button to measure the similarity between the output signal and a time-shifted version of itself.
        </li>
    </ul>
</body>
</html>
