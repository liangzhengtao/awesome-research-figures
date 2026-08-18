# Machine Learning Result Visualization

## When to Use

- Visualizing classification and regression results (confusion matrices, ROC curves)
- Plotting training/validation curves during model development
- Creating ablation study or hyperparameter sensitivity figures
- Comparing model performance across multiple metrics
- Presenting ML experimental results in academic papers

## Tools and Libraries

```
pip install matplotlib numpy scikit-learn seaborn pandas
```

## Step-by-Step Instructions

### 1. ML Visualization Defaults

```python
import matplotlib
matplotlib.use('Agg')
import matplotlib.pyplot as plt
import numpy as np
from sklearn.metrics import (confusion_matrix, roc_curve, precision_recall_curve,
                              auc, classification_report, ConfusionMatrixDisplay)

plt.rcParams.update({
    'font.family': 'serif',
    'font.serif': ['Times New Roman', 'DejaVu Serif'],
    'font.size': 10,
    'axes.labelsize': 10,
    'axes.titlesize': 11,
    'xtick.labelsize': 9,
    'ytick.labelsize': 9,
    'legend.fontsize': 8,
    'figure.dpi': 300,
    'savefig.dpi': 600,
    'savefig.bbox': 'tight',
    'axes.linewidth': 0.8,
    'xtick.direction': 'in',
    'ytick.direction': 'in',
})

COLORS = ['#0072B2', '#D55E00', '#009E73', '#CC79A7',
          '#E69F00', '#56B4E9', '#F0E442', '#000000']
FIG_SINGLE = (3.5, 2.8)
FIG_DOUBLE = (7.0, 4.5)
```

## Code Templates

### Template 1: Publication Confusion Matrix

```python
def plot_confusion_matrix(y_true, y_pred, class_names,
                           normalize='true', filename='confusion_matrix.pdf',
                           figsize=(3.5, 3.0), cmap='Blues'):
    """
    Publication-quality confusion matrix heatmap.

    Parameters
    ----------
    y_true : array-like
        Ground truth labels.
    y_pred : array-like
        Predicted labels.
    class_names : list of str
        Class names for axis labels.
    normalize : str or None
        'true' (recall), 'pred' (precision), 'all', or None.
    """
    cm = confusion_matrix(y_true, y_pred, normalize=normalize)

    fig, ax = plt.subplots(figsize=figsize)
    im = ax.imshow(cm, interpolation='nearest', cmap=cmap, vmin=0, vmax=1)
    ax.set_aspect('equal')

    # Colorbar
    cbar = fig.colorbar(im, ax=ax, shrink=0.8, pad=0.02)
    cbar.ax.tick_params(labelsize=8)
    cbar_label = {
        'true': 'Recall (Normalized by Row)',
        'pred': 'Precision (Normalized by Column)',
        'all': 'Normalized by Total',
    }.get(normalize, 'Count')
    cbar.set_label(cbar_label, fontsize=9)

    # Annotate cells
    thresh = cm.max() / 2.0
    for i in range(cm.shape[0]):
        for j in range(cm.shape[1]):
            val = cm[i, j]
            text = f'{val:.2f}' if normalize else f'{int(val)}'
            color = 'white' if val > thresh else 'black'
            ax.text(j, i, text, ha='center', va='center',
                    fontsize=8, color=color)

    ax.set_xticks(range(len(class_names)))
    ax.set_yticks(range(len(class_names)))
    ax.set_xticklabels(class_names, fontsize=8)
    ax.set_yticklabels(class_names, fontsize=8)
    ax.set_xlabel('Predicted Label', fontsize=9)
    ax.set_ylabel('True Label', fontsize=9)

    fig.savefig(filename, format='pdf')
    plt.close(fig)
    print(f"Saved: {filename}")

# Usage
if __name__ == '__main__':
    np.random.seed(42)
    classes = ['Cat 0', 'Cat 1', 'Cat 2', 'Cat 3']
    y_true = np.random.randint(0, 4, 200)
    y_pred = y_true.copy()
    noise = np.random.rand(200) < 0.15
    y_pred[noise] = np.random.randint(0, 4, noise.sum())
    plot_confusion_matrix(y_true, y_pred, classes)
```

### Template 2: ROC and PR Curves (Multi-class)

```python
def plot_roc_curves(y_true, y_score, class_names,
                    filename='roc_curves.pdf', figsize=FIG_SINGLE):
    """
    One-vs-rest ROC curves for multi-class classification.

    Parameters
    ----------
    y_true : array-like
        True integer labels.
    y_score : array-like, shape (n_samples, n_classes)
        Predicted probabilities.
    class_names : list of str
    """
    from sklearn.preprocessing import label_binarize

    n_classes = len(class_names)
    y_true_bin = label_binarize(y_true, classes=range(n_classes))

    fig, ax = plt.subplots(figsize=figsize)

    for i in range(n_classes):
        fpr, tpr, _ = roc_curve(y_true_bin[:, i], y_score[:, i])
        roc_auc = auc(fpr, tpr)
        ax.plot(fpr, tpr, color=COLORS[i % len(COLORS)],
                linewidth=1.5, label=f'{class_names[i]} (AUC={roc_auc:.3f})')

    ax.plot([0, 1], [0, 1], 'k--', linewidth=0.8, alpha=0.5)
    ax.set_xlabel('False Positive Rate')
    ax.set_ylabel('True Positive Rate')
    ax.set_xlim(-0.02, 1.02)
    ax.set_ylim(-0.02, 1.02)
    ax.legend(loc='lower right', framealpha=0.9, fontsize=7)
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)

    fig.savefig(filename, format='pdf')
    plt.close(fig)


def plot_pr_curves(y_true, y_score, class_names,
                    filename='pr_curves.pdf', figsize=FIG_SINGLE):
    """Precision-Recall curves for multi-class."""
    from sklearn.preprocessing import label_binarize

    n_classes = len(class_names)
    y_true_bin = label_binarize(y_true, classes=range(n_classes))

    fig, ax = plt.subplots(figsize=figsize)

    for i in range(n_classes):
        prec, rec, _ = precision_recall_curve(y_true_bin[:, i], y_score[:, i])
        pr_auc = auc(rec, prec)
        ax.plot(rec, prec, color=COLORS[i % len(COLORS)],
                linewidth=1.5, label=f'{class_names[i]} (AP={pr_auc:.3f})')

    ax.set_xlabel('Recall')
    ax.set_ylabel('Precision')
    ax.set_xlim(-0.02, 1.02)
    ax.set_ylim(-0.02, 1.02)
    ax.legend(loc='lower left', framealpha=0.9, fontsize=7)
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)

    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

### Template 3: Training Curves

```python
def plot_training_curves(train_losses, val_losses, train_accs=None,
                          val_accs=None, filename='training.pdf',
                          figsize=FIG_DOUBLE):
    """
    Training/validation loss and accuracy curves.

    Parameters
    ----------
    train_losses, val_losses : list of float
    train_accs, val_accs : list of float, optional
    """
    has_acc = train_accs is not None and val_accs is not None
    fig, axes = plt.subplots(1, 2 if has_acc else 1, figsize=figsize)
    if not has_acc:
        axes = [axes]

    epochs = range(1, len(train_losses) + 1)

    # Loss
    ax = axes[0]
    ax.plot(epochs, train_losses, color=COLORS[0], linewidth=1.5,
            label='Training Loss')
    ax.plot(epochs, val_losses, color=COLORS[1], linewidth=1.5,
            label='Validation Loss')
    ax.set_xlabel('Epoch')
    ax.set_ylabel('Loss')
    ax.legend(framealpha=0.9)
    ax.spines['top'].set_visible(False)
    ax.spines['right'].set_visible(False)

    # Mark best epoch
    best_epoch = np.argmin(val_losses) + 1
    best_val = min(val_losses)
    ax.axvline(x=best_epoch, color='gray', linestyle=':', alpha=0.5)
    ax.annotate(f'Best: epoch {best_epoch}',
                xy=(best_epoch, best_val), xytext=(best_epoch + 2, best_val + 0.1),
                fontsize=7, arrowprops=dict(arrowstyle='->', color='gray'))

    # Accuracy
    if has_acc:
        ax = axes[1]
        ax.plot(epochs, train_accs, color=COLORS[0], linewidth=1.5,
                label='Training Accuracy')
        ax.plot(epochs, val_accs, color=COLORS[1], linewidth=1.5,
                label='Validation Accuracy')
        ax.set_xlabel('Epoch')
        ax.set_ylabel('Accuracy')
        ax.legend(framealpha=0.9)
        ax.spines['top'].set_visible(False)
        ax.spines['right'].set_visible(False)

    fig.tight_layout()
    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

### Template 4: Hyperparameter Sensitivity Heatmap

```python
def plot_hyperparameter_heatmap(results, param1_name, param2_name,
                                 metric_name='Accuracy',
                                 filename='hyperparam_heatmap.pdf',
                                 figsize=(4.5, 3.5)):
    """
    Heatmap showing metric values for two hyperparameter combinations.

    Parameters
    ----------
    results : dict
        {(val1, val2): metric_value, ...}
    param1_name, param2_name : str
    """
    vals1 = sorted(set(k[0] for k in results.keys()))
    vals2 = sorted(set(k[1] for k in results.keys()))

    matrix = np.zeros((len(vals1), len(vals2)))
    for (v1, v2), val in results.items():
        i = vals1.index(v1)
        j = vals2.index(v2)
        matrix[i, j] = val

    fig, ax = plt.subplots(figsize=figsize)
    im = ax.imshow(matrix, cmap='RdYlGn', aspect='auto',
                   vmin=matrix.min(), vmax=matrix.max())

    cbar = fig.colorbar(im, ax=ax, shrink=0.8)
    cbar.set_label(metric_name, fontsize=9)

    # Annotate cells
    for i in range(len(vals1)):
        for j in range(len(vals2)):
            text = f'{matrix[i, j]:.3f}'
            color = 'white' if matrix[i, j] < (matrix.min() + matrix.max()) / 2 \
                    else 'black'
            ax.text(j, i, text, ha='center', va='center',
                    fontsize=7, color=color)

    ax.set_xticks(range(len(vals2)))
    ax.set_yticks(range(len(vals1)))
    ax.set_xticklabels([str(v) for v in vals2], fontsize=8)
    ax.set_yticklabels([str(v) for v in vals1], fontsize=8)
    ax.set_xlabel(param2_name, fontsize=9)
    ax.set_ylabel(param1_name, fontsize=9)

    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

### Template 5: Ablation Study Bar Chart

```python
def plot_ablation_study(components, metrics_dict, baseline,
                         filename='ablation.pdf', figsize=FIG_DOUBLE):
    """
    Bar chart showing ablation study results.

    Parameters
    ----------
    components : list of str
        Names of ablated components.
    metrics_dict : dict
        {metric_name: [values per ablation condition], ...}
    baseline : dict
        {metric_name: baseline_value, ...}
    """
    n_metrics = len(metrics_dict)
    n_components = len(components) + 1  # +1 for full model

    fig, axes = plt.subplots(1, n_metrics, figsize=figsize,
                              sharey=False)
    if n_metrics == 1:
        axes = [axes]

    for ax, (metric, values) in zip(axes, metrics_dict.items()):
        all_labels = ['Full Model'] + components
        all_values = [baseline[metric]] + values
        colors = [COLORS[0]] + [COLORS[1]] * len(components)

        bars = ax.barh(range(len(all_labels)), all_values,
                       color=colors, edgecolor='black', linewidth=0.5,
                       height=0.6, alpha=0.8)

        # Mark drops from baseline
        base_val = baseline[metric]
        for i, v in enumerate(all_values[1:], 1):
            drop = base_val - v
            if drop > 0:
                ax.annotate(f'-{drop:.1%}',
                           xy=(v, i), xytext=(v + 0.01, i),
                           fontsize=7, color=COLORS[1], va='center')

        ax.set_yticks(range(len(all_labels)))
        ax.set_yticklabels(all_labels, fontsize=8)
        ax.set_xlabel(metric, fontsize=9)
        ax.invert_yaxis()
        ax.spines['top'].set_visible(False)
        ax.spines['right'].set_visible(False)

    fig.tight_layout()
    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

### Template 6: Multi-Metric Radar Chart

```python
def plot_metric_radar(models, metrics_dict, filename='radar.pdf',
                       figsize=(4.0, 3.5)):
    """
    Radar (spider) chart comparing models across multiple metrics.

    Parameters
    ----------
    models : list of str
    metrics_dict : dict
        {model_name: [val1, val2, ...], ...}
    """
    categories = list(next(iter(metrics_dict.values())))
    n = len(categories)
    angles = np.linspace(0, 2 * np.pi, n, endpoint=False).tolist()
    angles += angles[:1]

    fig, ax = plt.subplots(figsize=figsize, subplot_kw=dict(polar=True))

    for i, (model, values) in enumerate(metrics_dict.items()):
        vals = list(values.values()) if isinstance(values, dict) else list(values)
        vals += vals[:1]
        ax.plot(angles, vals, color=COLORS[i % len(COLORS)],
                linewidth=1.5, label=model)
        ax.fill(angles, vals, color=COLORS[i % len(COLORS)], alpha=0.1)

    ax.set_xticks(angles[:-1])
    ax.set_xticklabels(categories, fontsize=8)
    ax.set_ylim(0, 1)
    ax.legend(loc='upper right', bbox_to_anchor=(1.3, 1.1),
              fontsize=8, framealpha=0.9)

    fig.savefig(filename, format='pdf')
    plt.close(fig)
```

## Style Specifications

| Element | Value |
|---------|-------|
| Confusion matrix font | 8 pt, white on dark / black on light |
| ROC/PR curve line width | 1.5 pt |
| Legend entries | 7-8 pt |
| Bar chart capsize | 2 pt |
| Grid lines | Disabled by default |
| Axis spines | Remove top and right |
| Color palette | Wong 2011 colorblind-safe |

## Common Pitfalls

1. **Unnormalized confusion matrix misleading**: Always show `normalize='true'` alongside raw counts
2. **Overlapping ROC curves**: Add AUC to legend; consider inset for crowded region
3. **Training curve overfitting not shown**: Always include validation curve
4. **Too many lines in one plot**: Split into subplots if > 6 models
5. **Missing baseline in ablation**: Always include a "full model" reference bar
6. **Hyperparameter heatmap without annotation**: Always show numeric values in cells
7. **Radar chart with too many axes**: Limit to 6-8 metrics for readability

## Journal-Specific Tips

- **NeurIPS/ICML/ICLR**: Use standard metrics (accuracy, F1, AUC); include confidence intervals
- **IEEE TPAMI**: Confusion matrices should include per-class precision/recall
- **Nature Machine Intelligence**: Provide source code for figure generation
- **JMLR**: Open access figures; provide raw data as CSV
- **General**: Include error bars or confidence intervals from multiple runs/seeds

---

## 中文版本

### 使用场景
- 可视化分类和回归结果（混淆矩阵、ROC 曲线）
- 绘制训练/验证曲线
- 创建消融实验或超参数敏感性图表
- 比较多指标下的模型性能
- 在学术论文中展示 ML 实验结果

### 工具库
```
pip install matplotlib numpy scikit-learn seaborn pandas
```

### 代码模板说明
- **模板 1**：出版级混淆矩阵（支持按行/列/全局归一化，自动标注数值和颜色）
- **模板 2**：多类别 ROC 曲线和 PR 曲线（one-vs-rest，带 AUC 标注）
- **模板 3**：训练曲线（损失 + 精度双面板，标注最佳 epoch）
- **模板 4**：超参数敏感性热力图（两参数组合的指标矩阵）
- **模板 5**：消融实验柱状图（水平条形图，标注相对基线的下降百分比）
- **模板 6**：多指标雷达图（蜘蛛图比较多个模型）

### 常见陷阱
1. **未归一化的混淆矩阵具有误导性**：始终同时展示 `normalize='true'` 和原始计数
2. **ROC 曲线重叠**：在图例中添加 AUC 值；考虑局部放大插图
3. **训练曲线未展示过拟合**：始终包含验证曲线
4. **单图线条过多**：超过 6 个模型时拆分为子图
5. **消融实验缺少基线**：始终包含"完整模型"参考柱
6. **超参数热力图无标注**：始终在单元格中显示数值
7. **雷达图轴过多**：限制在 6-8 个指标以保证可读性
