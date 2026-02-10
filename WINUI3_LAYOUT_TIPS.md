# WinUI 3 レイアウト調整メモ

## 要件
- 1列目 (`Grid.Column=0`) をホバー可能領域として扱う。
- 3列目 (`Grid.Column=2`) の要素を、現在より上方向に配置したい。

## 推奨パターン

`Grid` 自体は列構成を維持し、3列目の要素側で `VerticalAlignment="Top"` と `Margin` を使って上に寄せる。
ホバー処理は1列目に `Border` を置いて `PointerEntered/PointerExited` を受けると扱いやすい。

```xml
<Grid>
    <Grid.ColumnDefinitions>
        <ColumnDefinition Width="*"/>
        <ColumnDefinition Width="Auto"/>
        <ColumnDefinition Width="Auto"/>
    </Grid.ColumnDefinitions>

    <!-- 1列目: ホバー検知領域 -->
    <Border Grid.Column="0"
            Background="Transparent"
            PointerEntered="FirstColumn_PointerEntered"
            PointerExited="FirstColumn_PointerExited"/>

    <!-- 3列目: 上寄せしたい要素 -->
    <StackPanel Grid.Column="2"
                VerticalAlignment="Top"
                Margin="0,4,0,0">
        <!-- 必要なコントロール -->
    </StackPanel>
</Grid>
```

## 補足
- 3列目を「さらに上」に動かすには `Margin="0,-4,0,0"` のように上マージンを負値にする方法もある。
- 行全体に対して確実に上へ寄せたい場合は、該当行の `RowDefinition Height="Auto"` も併せて確認する。
