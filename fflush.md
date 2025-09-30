バッファ（データを一時的に記憶する場所）に貯まっている内容を、強制的に表示する命令。
※この指示が無い場合は、タイミングを見てまとめて画面に表示させる仕組みになっているが、
ゲームなどでは「改行が無い出力」が多い（同じ場所に描画しなおす）ため、
fflush(stdout)を入れて、出した瞬間に画面に反映させる必要がある。

以下、ChatGPTによる生成コード。バッファに貯まるのを待たずに、毎回1文字ずつ表示させるので遅い。
バッファに貯まるまで待つ場合は、表示させるまでの時間が少し長いが、一気に表示させるので速い。

#include <stdio.h>
#include <unistd.h>   // usleep を使う（Linux / Mac）
// Windowsなら #include <windows.h> として Sleep() を使う

int main(void) {
    int i;

    // ---- 遅い例：毎回fflush ----
    for (i = 0; i < 20; i++) {
        printf("■");        // ピース表示
        fflush(stdout);     // 毎回すぐに出す
        usleep(100000);     // 0.1秒待つ（Windowsなら Sleep(100)）
    }
    printf("\n");

    // ---- 速い例：バッファ任せ ----
    for (i = 0; i < 20; i++) {
        printf("■");        // バッファに溜まる
        usleep(100000);     // 0.1秒待つ
        // fflushなし → 最後まで表示されない
    }
    printf("\n");

    return 0;
}
