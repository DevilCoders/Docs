A program to normalized and upload loops to S3 and update loops metadata table.

How to convert textures before upload:

`ls *.wav | while read f; do ffmpeg -hide_banner -nostdin -y -i "$f" -acodec pcm_s16le -ar 44100 "copy-$f" ; done`
`ls copy-*.wav | while read f ; do mv "$f" "${f:5}"; done`
