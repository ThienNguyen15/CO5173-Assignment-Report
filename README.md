# Báo cáo Bài tập lớn CO5173: MarketPulse 360

Mã nguồn LaTeX của báo cáo bài tập lớn môn **Kỹ thuật Dữ liệu (CO5173)**, Nhóm 09, Khoa Khoa học và Kỹ thuật Máy tính, Trường Đại học Bách Khoa, ĐHQG-HCM. Báo cáo trình bày **MarketPulse 360**, hệ thống Kỹ thuật Dữ liệu cho phân tích marketing đa kênh.

Báo cáo được biên dịch bằng **LuaLaTeX**. File `latexmkrc` đã cấu hình sẵn, chỉ cần một lệnh `latexmk` là ra PDF.

## Yêu cầu

| Thành phần | Phiên bản đã kiểm thử | Vai trò |
|---|---|---|
| MiKTeX (Windows) hoặc TeX Live / MacTeX (Linux, macOS) | MiKTeX 25.12 (LuaHBTeX 1.24) | LuaLaTeX, BibTeX và các gói LaTeX |
| latexmk | 4.88 | Tự chạy LuaLaTeX và BibTeX đủ số lượt cần thiết |
| Perl 5 | 5.38 | latexmk là một script Perl (chỉ cần cài riêng trên Windows) |
| Git | 2.50 | Lấy mã nguồn |
| VS Code + LaTeX Workshop | không bắt buộc | Soạn thảo và build ngay trong editor |

## Cài đặt

### Windows

1. Cài **MiKTeX** từ <https://miktex.org/download>. Ở bước cài đặt, chọn *Install missing packages on-the-fly*: **Yes** để MiKTeX tự tải các gói còn thiếu trong lần build đầu.
2. Mở **MiKTeX Console** → *Updates* → *Check for updates* → *Update now*.
3. Cài **Strawberry Perl** từ <https://strawberryperl.com>. Nếu lệnh `perl -v` đã chạy được (ví dụ Perl đi kèm Git for Windows), có thể bỏ qua bước này.
4. Mở một cửa sổ terminal mới và kiểm tra:

   ```powershell
   lualatex --version
   latexmk -v
   perl -v
   ```

Hoặc cài nhanh bằng `winget`:

```powershell
winget install --id MiKTeX.MiKTeX
winget install --id StrawberryPerl.StrawberryPerl
```

### macOS

```bash
brew install --cask mactex-no-gui
```

MacTeX có sẵn LuaLaTeX, latexmk và Perl.

### Linux (Ubuntu/Debian)

```bash
sudo apt install texlive-full latexmk
```

## Build báo cáo

```bash
git clone https://github.com/ThienNguyen15/CO5173-Assignment-Report.git
cd CO5173-Assignment-Report
latexmk -pdf -outdir=build CO5173_Group09_Report.tex
```

Kết quả: `build/CO5173_Group09_Report.pdf`. Tên file chứa mã nhóm theo đúng yêu cầu nộp bài của môn học, nên có thể nộp trực tiếp mà không cần đổi tên. Mọi file trung gian (`.aux`, `.log`, `.bbl`, ...) cũng nằm trong `build/`, thư mục gốc luôn sạch.

Lệnh dùng cờ `-pdf` nhưng thực tế chạy **LuaLaTeX**: dòng `$pdflatex = 'lualatex %O %S';` trong `latexmkrc` thay `pdflatex` bằng `lualatex`. latexmk tự chạy LuaLaTeX, BibTeX rồi LuaLaTeX thêm cho tới khi mục lục và tham chiếu ổn định. Lần build đầu tiên có thể mất vài phút (tạo bộ nhớ đệm phông chữ, tải gói còn thiếu); các lần sau mất khoảng 45 giây.

| Mục đích | Lệnh |
|---|---|
| Build PDF | `latexmk -pdf -outdir=build CO5173_Group09_Report.tex` |
| Tự build lại mỗi khi lưu file | `latexmk -pdf -pvc -outdir=build CO5173_Group09_Report.tex` |
| Xóa file trung gian, giữ lại PDF | `latexmk -c -outdir=build CO5173_Group09_Report.tex` |
| Xóa toàn bộ kết quả build | `latexmk -C -outdir=build CO5173_Group09_Report.tex` |

### Build trong VS Code (LaTeX Workshop)

1. Cài extension **LaTeX Workshop**.
2. Thêm vào `.vscode/settings.json` của workspace để file build không rơi ra thư mục gốc:

   ```json
   { "latex-workshop.latex.outDir": "%DIR%/build" }
   ```

3. Mở `CO5173_Group09_Report.tex`, chọn *Build LaTeX project* (`Ctrl+Alt+B`). Recipe mặc định gọi `latexmk -pdf`, nên cũng tự chạy LuaLaTeX nhờ `latexmkrc`.

### Build trên Overleaf

1. *New Project* → *Upload Project*, tải lên file ZIP của repo (trên GitHub: *Code* → *Download ZIP*).
2. *Menu* → *Settings*: chọn **Compiler: LuaLaTeX** và **Main document: CO5173_Group09_Report.tex**.

## Cấu trúc thư mục

```text
.
├── CO5173_Group09_Report.tex           # File chính: preamble, trang bìa, mục lục và 6 chương
├── latexmkrc                           # Cấu hình latexmk: biên dịch bằng LuaLaTeX
├── refs.bib                            # Tài liệu tham khảo (BibTeX, kiểu IEEE)
├── hcmut.png                           # Logo trang bìa
├── all-relational-schemas.excalidraw   # Sơ đồ quan hệ gốc của toàn hệ thống
├── Bibliocosas/
│   └── glossary.tex                    # Khai báo thuật ngữ và từ viết tắt
└── chapters/
    ├── Chap1.tex ... Chap6.tex         # Nội dung 6 chương
    ├── Figs/                           # Hình vẽ TikZ (sửa trực tiếp bằng code)
    └── Pics/                           # Ảnh lược đồ xuất từ file Excalidraw
```

| File | Chương |
|---|---|
| `chapters/Chap1.tex` | 1. Giới thiệu đề tài |
| `chapters/Chap2.tex` | 2. Dữ liệu và kiến trúc giải pháp |
| `chapters/Chap3.tex` | 3. Công nghệ quản lý và xử lý dữ liệu |
| `chapters/Chap4.tex` | 4. Ứng dụng Marketing Command Center |
| `chapters/Chap5.tex` | 5. Đánh giá thực nghiệm |
| `chapters/Chap6.tex` | 6. Thách thức và kết luận |

## Quy ước khi viết

- **Một đoạn một dòng.** Mỗi đoạn văn và mỗi `\item` viết trên một dòng trong file `.tex`; các đoạn cách nhau một dòng trống.
- **Không dùng gạch dài `---`.** Dùng dấu phẩy, ngoặc đơn, dấu hai chấm hoặc tách câu. Gạch ngắn `--` chỉ dùng cho khoảng, ví dụ `20:00--22:00`.
- **Đề mục.** Chỉ chương và mục (1.1, 1.2, ...) được đánh số và đưa vào mục lục. `\subsection` không đánh số, tiêu đề phải nằm gọn trên một dòng (khoảng 45 ký tự).
- **Dòng cuối của đoạn luôn có ít nhất 2 từ.** Quy tắc này nằm trong preamble và tự áp dụng khi build bằng LuaLaTeX, không cần chèn `~`. Nếu một ô bảng quá hẹp để giữ hai từ cuối trên cùng một dòng, hãy nới cột hoặc viết lại ô đó.
- **Định danh kỹ thuật** (tên bảng, cột, topic) đặt trong `\texttt{...}`; dấu gạch dưới viết `\_`, LaTeX được phép ngắt dòng sau dấu này. Không dùng `\_` bên trong công thức toán.
- **Số liệu** viết bằng `\num{...}` để có định dạng Việt Nam: `\num{1200225}` thành 1.200.225, `\num{79812.6}` thành 79.812,6.
- **Nhãn và tham chiếu.** Đặt nhãn với tiền tố `chap:`, `sec:`, `fig:`, `tab:`; tham chiếu bằng `Hình~\ref{...}`, `Bảng~\ref{...}`; trích dẫn bằng `\cite{...}` với khóa có trong `refs.bib`.
- **Hình mới.** Hình TikZ đặt trong `chapters/Figs/` và dùng các style có sẵn (`mpbox`, `mphead`, `mpzone`, `mparrow`); xuống dòng trong khung bằng `\\` ở chỗ ngắt tự nhiên. Ảnh đặt trong `chapters/Pics/`.

## Sơ đồ quan hệ (Excalidraw)

`all-relational-schemas.excalidraw` là sơ đồ gốc của toàn bộ lược đồ dữ liệu. Mở bằng extension **Excalidraw** trong VS Code, hoặc tại <https://excalidraw.com> (*Open*, `Ctrl+O`).

Các ảnh trong `chapters/Pics/` được xuất từ sơ đồ này. Lược đồ nào quá rộng được tách thành hai ảnh (`-1`, `-2`), mỗi ảnh chứa hai cột bảng, để chữ khi in ra vẫn đạt khoảng 7–8pt:

| Ảnh | Nội dung | Dùng ở |
|---|---|---|
| `schema-bronze.png` | Tầng Bronze | Chương 2 |
| `schema-silver-1.png` | Silver: `customer_events`, `customers`, `campaigns`, `products` | Chương 2 |
| `schema-silver-2.png` | Silver: `ad_spend_daily`, `quality_summary` | Chương 2 |
| `schema-gold-1.png` | Mô hình dbt: `customers`, `customer_360`, `campaigns`, `commerce_daily`, `cohort_retention` | Chương 3 |
| `schema-gold-2.png` | Mô hình dbt: `campaign_performance_daily`, `campaign_dashboard`, `funnel_daily`, `attribution_daily` | Chương 3 |
| `schema-postgres-1.png` | PostgreSQL: hai cột bảng bên trái của sơ đồ | Chương 4 |
| `schema-postgres-2.png` | PostgreSQL: cột bảng bên phải (kiểm toán, cảnh báo, sổ cái công bố) | Chương 4 |
| `schema-clickhouse-1.png` | ClickHouse: nhật ký công bố và journey sidecar | Chương 4 |
| `schema-clickhouse-2.png` | ClickHouse: kho trực tiếp `marketpulse_live` | Chương 4 |

Khi sửa sơ đồ: chọn đúng các bảng của phần cần xuất (với ảnh tách đôi, chỉ chọn các bảng của phần đó) → *Export image* → bật *Only selected*, tỉ lệ **3×**, nền trắng → lưu đè đúng tên file cũ trong `chapters/Pics/`. Build lại là báo cáo cập nhật.

## Ghi chú kỹ thuật

- **Phông chữ:** Latin Modern (OpenType, nạp qua `fontspec`), hiển thị đủ dấu tiếng Việt.
- **Quy tắc dòng cuối:** viết bằng Lua trong preamble của `CO5173_Group09_Report.tex` (callback `pre_linebreak_filter`), chỉ hoạt động với LuaLaTeX.
- **Dự phòng pdfLaTeX:** nếu lỡ biên dịch bằng pdfLaTeX, preamble tự chuyển sang gói `vietnam` (vntex) và gói `impnattypo`. Báo cáo vẫn ra PDF, nhưng quy tắc dòng cuối chỉ ở mức khuyến khích. Bản chính thức luôn build bằng LuaLaTeX.

## Xử lý sự cố

| Hiện tượng | Cách xử lý |
|---|---|
| `latexmk` báo không tìm thấy Perl | Cài Strawberry Perl, mở lại terminal |
| `major issue: So far, you have not checked for MiKTeX updates` | MiKTeX Console → *Updates* → *Check for updates* |
| MiKTeX hỏi cài thêm gói | Chọn *Install*, hoặc bật tự cài gói trong MiKTeX Console → *Settings* |
| Lần build đầu tiên rất lâu | LuaLaTeX đang tạo bộ nhớ đệm phông chữ; các lần sau nhanh hơn |
| Tham chiếu hiện `??` hoặc trích dẫn hiện `[?]` | Build lại bằng `latexmk` (tự chạy đủ số lượt); kiểm tra khóa trong `refs.bib` |
| File `.aux`, `.log` xuất hiện cạnh `CO5173_Group09_Report.tex` | Lệnh build thiếu `-outdir=build`, hoặc LaTeX Workshop chưa đặt `outDir`; xóa các file đó rồi build lại |
