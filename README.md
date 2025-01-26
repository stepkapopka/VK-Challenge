# VK-Challenge
Постороение графика на основе полученных метрик VMAF для отбора на стажировку "Инженер по автоматизации тестирования"
![image](https://github.com/user-attachments/assets/6b5aa24d-c95e-4595-a446-c51cef964835)

## Использованные команды
**Получение первых 30 секунд**
```console
ffmpeg -i "big_buck_bunny_1080p24.y4m" -t 30 -c:v copy -c:a copy "big_buck_bunny_30s.y4m"
```
**Кодирование, используя кодек h264**
```console
ffmpeg -i "big_buck_bunny_1080p24.y4m" -vf scale=256:144 -c:v libx264 -preset veryfast -crf 23 "output_144p.mp4"
ffmpeg -i "big_buck_bunny_1080p24.y4m" -vf scale=426:240 -c:v libx264 -preset veryfast -crf 23 "output_240p.mp4"
ffmpeg -i "big_buck_bunny_1080p24.y4m" -vf scale=640:360 -c:v libx264 -preset veryfast -crf 23 "output_360p.mp4"
ffmpeg -i "big_buck_bunny_1080p24.y4m" -vf scale=854:480 -c:v libx264 -preset veryfast -crf 23 "output_480p.mp4"
ffmpeg -i "big_buck_bunny_1080p24.y4m" -vf scale=1280:720 -c:v libx264 -preset veryfast -crf 23 "output_720p.mp4"
ffmpeg -i "big_buck_bunny_1080p24.y4m" -vf scale=1920:1080 -c:v libx264 -preset veryfast -crf 23 "output_1080p.mp4"
```
**Оценка качества с помощью метрики VMAF**
```console
ffmpeg -i "output_144p.mp4" -i "big_buck_bunny_1080p24.y4m" -filter_complex "[0:v]scale=1920:1080[main];[main][1:v]libvmaf='n_threads=10':log_path=vmafOutput.txt" -f null -
ffmpeg -i "output_240p.mp4" -i "big_buck_bunny_1080p24.y4m" -filter_complex "[0:v]scale=1920:1080[main];[main][1:v]libvmaf='n_threads=10':log_path=vmafOutput1.txt" -f null -
ffmpeg -i "output_360p.mp4" -i "big_buck_bunny_1080p24.y4m" -filter_complex "[0:v]scale=1920:1080[main];[main][1:v]libvmaf='n_threads=10':log_path=vmafOutput2.txt" -f null -
ffmpeg -i "output_480p.mp4" -i "big_buck_bunny_1080p24.y4m" -filter_complex "[0:v]scale=1920:1080[main];[main][1:v]libvmaf='n_threads=10':log_path=vmafOutput3.txt" -f null -
ffmpeg -i "output_720p.mp4" -i "big_buck_bunny_1080p24.y4m" -filter_complex "[0:v]scale=1920:1080[main];[main][1:v]libvmaf='n_threads=10':log_path=vmafOutput4.txt" -f null -
ffmpeg -i "output_1080p.mp4" -i "big_buck_bunny_1080p24.y4m" -filter_complex "[0:v]scale=1920:1080[main];[main][1:v]libvmaf='n_threads=10':log_path=vmafOutput5.txt" -f null -
```
Полученные лог-файлы находяся в репозитории, а также представлен файл для построения графика на основе полученных лог-файлов (`graph_generate.ipynb`)
