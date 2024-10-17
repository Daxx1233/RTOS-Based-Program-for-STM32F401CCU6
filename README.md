# Praktikum RTOS - SEMESTER 5 (3 Teknik Komputer A)
- Triyas Rahmadiyanti (3222600001)
- Duta Fithra Qolby (3222600003)
# Task 2 - Hello World for RTOS
## Deskripsi Projek
Alur eksekusi projek ini dimulai dengan inisialisasi sistem dan periferal dalam fungsi main(), diikuti dengan inisialisasi kernel FreeRTOS (osKernelInitialize()) dan pembuatan beberapa tugas untuk fungsi yang berbeda. 
Scheduler kemudian dijalankan menggunakan osKernelStart(). 
Setiap tugas berjalan dalam loop tak terbatas (for(;;)) untuk menangani fungsinya masing-masing, seperti membaca nilai ADC, memperbarui level LED, atau mengelola komunikasi UART. Pengguna dapat berinteraksi dengan sistem melalui penekanan tombol atau mengirim input tertentu melalui UART untuk memicu perilaku yang berbeda. 
![31445740-a9f7-4f79-8971-a7d1dfceb795](https://github.com/user-attachments/assets/d675b3a2-c2dc-49ed-9301-55796a2d7074)
1. Dilakukan inisialisasi berbagai periferal seperti GPIO, ADC, I2C, dan UART, serta konfigurasi clock sistem. Kode juga mendefinisikan variabel global seperti x_val (nilai pembacaan ADC) dan button1_pressed (indikator status tombol), serta beberapa handle tugas (defaultTaskHandle, pickButtonTaskHandle, dll.) untuk mengelola tugas-tugas yang dibuat di lingkungan FreeRTOS.
2. Periferal ADC, I2C, dan UART diinisialisasi dan dikonfigurasi melalui handle hadc1, hi2c1, dan huart2.
3. Tugas StartDefaultTask adalah tugas dasar yang hanya melakukan delay tak terbatas (osDelay(1);), sedangkan tugas pickButton memantau status tombol yang terhubung ke pin GPIO dan menandai button1_pressed sebagai 1 saat tombol ditekan.
4. Tugas getADC membaca nilai ADC secara berkala dan menyimpannya ke variabel x_val. Tugas LEDlevel mengontrol level LED berdasarkan nilai x_val dan status tombol. Jika tombol ditekan, tugas ini akan menyalakan LED berdasarkan nilai x_val dan memberikan delay pendek (osDelay(300);) sebelum mematikan LED sementara. Jika tombol tidak ditekan, LED hanya akan menyala sesuai nilai x_val.
5. Tugas dispUART memantau input UART dari pengguna dan mengirimkan respons sesuai data yang diterima (choice). Jika pengguna mengirim ‘1’, tugas ini akan mengirimkan nilai tegangan saat ini (x_val) melalui UART, dan jika pengguna mengirim ‘2’, sistem akan mengirim pesan “HELLO WORLD” dan menampilkan menu kembali. Tugas ini juga memeriksa apakah tombol ditekan dan akan mengirim pesan (“Button1 pressed\r\n”) melalui UART jika tombol ditekan.
6. Kode ini juga memiliki beberapa fungsi pembantu seperti Light_LED() yang mengatur lima LED berdasarkan nilai x_val, Tf_LED() yang mematikan semua LED, dan Menu_Display() yang menampilkan nilai tegangan saat ini melalui UART.
7. Selain itu, terdapat fungsi konfigurasi periferal seperti SystemClock_Config() untuk konfigurasi clock sistem, MX_GPIO_Init() untuk inisialisasi GPIO, MX_ADC1_Init() untuk konfigurasi ADC, MX_I2C1_Init() untuk konfigurasi I2C, dan MX_USART2_UART_Init() untuk konfigurasi UART.
8. Callback timer (HAL_TIM_PeriodElapsedCallback()) digunakan untuk meningkatkan tick sistem FreeRTOS ketika interupsi timer (TIM4) terjadi. Kode juga dilengkapi dengan penanganan error (Error_Handler()) untuk menghentikan sistem jika terjadi error, dan assert_failed() sebagai fungsi placeholder ketika assert gagal saat pengembangan.

# Gambar Hardware
![image](https://github.com/user-attachments/assets/1ec98083-0b04-4144-858b-adb18a42cd5c)

# GIF Hardware 
https://github.com/user-attachments/assets/fdc241b0-bc8f-4988-9a06-5580b8260904


https://github.com/user-attachments/assets/8b635266-8409-4317-b9e0-a9834f8d3c74



