# Arduino-digital-Delay

program untuk mengontrol pedal efek untuk gitar, suara, synthesizer, dll. Program ini disebut "echoTrek" dan merupakan versi 1.0 yang dibuat oleh J. CesarSound pada Januari 2021. Program ini dapat digunakan dengan Arduino UNO R3 / NANO / PRO MINI dan terdiri dari beberapa fungsi.

Pada fungsi setup(), pin time_selector diatur sebagai input pull-up, dan DDRD dan DDRB diatur agar dapat mengeluarkan output PWM pada pin D5. Timer 1 disetel pada frekuensi 16.384kHz dan referensi analog disetel ke tegangan 1,1v. Selanjutnya, fungsi up_time() dipanggil untuk mengatur delay pada efek.

Fungsi loop() pertama-tama memeriksa apakah tombol pushbutton time_selector ditekan. Jika ditekan, maka up_time() akan dipanggil untuk mengatur delay sesuai dengan waktu yang dipilih. Jika tidak, maka led di pin 13 akan dimatikan. Selain itu, fungsi juga memeriksa apakah efek diatur pada mode reverse speech dan menyalakan lampu indikator TX.

Fungsi sampling() memetakan input analog dari pin audio_in dan menghitung nilai delay pada fungsi delay_sound(). Selanjutnya, fungsi analogWrite() digunakan untuk menulis output ke pin 5.

Fungsi delay_sound() memperbarui buffer delay delay_data[] dan delay_data_1[] sesuai dengan nilai input yang diberikan. Jika efek diatur pada mode reverse speech, maka output akan diberikan dengan urutan yang terbalik. Selanjutnya, nilai dari d_val disetel ke buffer delay.

Fungsi up_time() mengatur delay yang digunakan pada efek berdasarkan waktu yang dipilih pada tombol pushbutton. Fungsi ini menggunakan noInterrupts() untuk mematikan interupsi sementara sebelum mengatur waktu delay pada d_time dan mode reverse pada rev. Kemudian, fungsi memanggil interrupts() untuk mengaktifkan kembali interupsi.

Fungsi InitTimer1() mengatur timer 1 pada frekuensi 16.384kHz dan mengaktifkan interupsi. Fungsi ISR(TIMER1_COMPA_vect) dipanggil pada setiap kali timer mencapai nilai OCR1A. Fungsi ini akan memanggil sampling().

Terakhir, fungsi setPwmFrequency() digunakan untuk mengatur output PWM pada pin 5 dan 6. Fungsi ini menggunakan prescaler untuk mengatur frekuensi output.
