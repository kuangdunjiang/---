package jfreechart;

import java.awt.Font;
import java.io.FileOutputStream;
import java.io.IOException;
import java.io.OutputStream;

import javax.servlet.ServletException;
import javax.servlet.ServletOutputStream;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import org.jfree.chart.ChartFactory;
import org.jfree.chart.ChartUtilities;
import org.jfree.chart.JFreeChart;
import org.jfree.chart.StandardChartTheme;
import org.jfree.chart.plot.PlotOrientation;
import org.jfree.data.category.DefaultCategoryDataset;

public class CharServlet extends HttpServlet {

  
	private static final long serialVersionUID = 1L;

	public void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		DefaultCategoryDataset categoryDataset = new DefaultCategoryDataset();
		categoryDataset.addValue(100, "lenovo", "联想");
		categoryDataset.addValue(150, "apple", "苹果");
		categoryDataset.addValue(200, "nokia", "诺基亚");
		
		StandardChartTheme chartTheme = new StandardChartTheme("");
		chartTheme.setExtraLargeFont(new Font("微软雅黑",Font.BOLD,32));
		chartTheme.setLargeFont(new Font("微软雅黑", Font.BOLD, 20));
		chartTheme.setRegularFont(new Font("微软雅黑",Font.BOLD,20));
		ChartFactory.setChartTheme(chartTheme);
		
		
		JFreeChart chart = ChartFactory.createBarChart3D("手机占有率", "公司名称", "占有率", categoryDataset, PlotOrientation.VERTICAL, true, false, false);
		
		OutputStream outputStream = response.getOutputStream();
		ChartUtilities.writeChartAsJPEG(outputStream, chart, 500, 500);
		outputStream.close();
		
		
		
		
		
		
	}

}
