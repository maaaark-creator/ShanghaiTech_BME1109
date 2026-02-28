import wfdb
record_ecg = wfdb.rdrecord('118', pn_dir='mitdb')
ecg = record_ecg.p_signal[:, 0]   # 单导联
fs = record_ecg.fs
record_ma = wfdb.rdrecord('ma', pn_dir='nstdb')
ma_noise = record_ma.p_signal[:, 0]
import numpy as np

L = min(len(ecg), len(ma_noise))
ecg = ecg[:L]
ma_noise = ma_noise[:L]
def add_noise_with_snr(signal, noise, snr_db):
    sig_power = np.mean(signal ** 2)
    noise_power = np.mean(noise ** 2)
    k = np.sqrt(sig_power / (noise_power * 10**(snr_db / 10)))
    return signal + k * noise

ecg_noisy = add_noise_with_snr(ecg, ma_noise, snr_db=6)
import matplotlib.pyplot as plt
duration = 10  # 秒
N = int(duration * fs)

ecg_10s = ecg_noisy[:N]
t_10s = np.arange(N) / fs

plt.figure(figsize=(10, 4))
plt.plot(t_10s, ecg_10s)
plt.xlabel("Time (s)")
plt.ylabel("Amplitude (mV)")
plt.title("ECG Signal (First 10 Seconds)")
plt.grid(True)
plt.show()

