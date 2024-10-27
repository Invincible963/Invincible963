clc; close all; clear all;

M = 2;                   % Modulation alphabet size
bps = log2(M);            % Bits per symbol
phOffset = 0;             % Phase offset
bitdata = int2bit(0,bps); % Generate one symbol to modulate
%Modulate the data symbols.
 pskmod(bitdata,M,phOffset,"bin",InputType="bit",PlotConstellation=true);
 data = randi([0 M-1],1000,1);
txSig =pskmod(data,M);
%Pass the signal through a noisy channel.
%scatterplot(txSig)
 title('Transmited signal');
%title('Transmitter 64-QAM constellation');
for snr=1:5:30
    rxSig = awgn(txSig,snr);
    %Plot the constellation diagram.
    scatterplot(rxSig);
  title(['Recieved signal with SNR=',num2str(snr),'(ROHIT PATIL Roll no=44 TE-A)']);
end
