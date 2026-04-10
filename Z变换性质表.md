Here is the markdown transcription of the Z-Transform Properties table from the image.

### Z-Transform Properties & ROC (Z变换性质表)

**Definitions:**

- $X(z) = \mathscr{Z}\{x[k]\}, \quad R_x = \{z; R_{x-} < |z| < R_{x+}\}$
    
- $Y(z) = \mathscr{Z}\{y[k]\}, \quad R_y = \{z; R_{y-} < |z| < R_{y+}\}$
    

| **性质 (Property)**                                 | **序列 (Sequence)** | **z变换 (Z-Transform)** | **ROC (Region of Convergence)**                                            |
| ------------------------------------------------- | ----------------- | --------------------- | -------------------------------------------------------------------------- |
| **线性特性**<br><br>  <br><br>(Linearity)             | $ax[k] + by[k]$   | $aX(z) + bY(z)$       | $R_x \cap R_y$                                                             |
| **共轭特性**<br><br>  <br><br>(Conjugation)           | $x^*[k]$          | $X^*(z^*)$            | $R_x$                                                                      |
| **翻转特性**<br><br>  <br><br>(Time Reversal)         | $x[-k]$           | $X(1/z)$              | $1/R_{x+} <                                                                |
| **位移特性**<br><br>  <br><br>(Time Shifting)         | $x[k-n]$          | $z^{-n}X(z)$          | $R_x$, 除了 $z=0$ 或 $z=\infty$<br><br>  <br><br>(Except $z=0$ or $z=\infty$) |
| **卷积特性**<br><br>  <br><br>(Convolution)           | $x[k] * y[k]$     | $X(z)Y(z)$            | $R_x \cap R_y$                                                             |
| **指数加权**<br><br>  <br><br>(Exponential Weighting) | $a^k x[k]$        | $X(z/a)$              | $                                                                          |

---

### 📝 Key Notes on ROC Changes:

1. **Linearity & Convolution:** The new ROC is the **intersection** ($\cap$) of the individual ROCs. If the intersection is empty, the Z-transform does not exist.
    
2. **Time Reversal:** The ROC is inverted. If the original was an annulus $a < |z| < b$, the new ROC is $\frac{1}{b} < |z| < \frac{1}{a}$.
    
3. **Time Shifting:** The ROC remains mostly the same, but depending on whether $n$ is positive (delay) or negative (advance), points at **origin ($z=0$)** or **infinity ($z=\infty$)** might be added or removed from the ROC.
    
4. **Exponential Weighting:** The ROC scales by the magnitude of $a$. The new boundaries become $|a|R_{x-} < |z| < |a|R_{x+}$.
    

**Would you like to see a specific calculation example for the "Exponential Weighting" property?**